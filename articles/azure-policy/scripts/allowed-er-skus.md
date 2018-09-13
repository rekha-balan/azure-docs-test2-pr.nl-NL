---
title: Azure Policy json sample - Allowed Express Route SKUs | Microsoft Docs
description: This json sample policy requires that Express Routes use an approved SKU.
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
ms.openlocfilehash: b4176d39bc6b5bffe11794080adde12fdb0c1731
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969114"
---
# <a name="allowed-express-route-skus"></a><span data-ttu-id="ef8a8-103">Allowed Express Route SKUs</span><span class="sxs-lookup"><span data-stu-id="ef8a8-103">Allowed Express Route SKUs</span></span>

<span data-ttu-id="ef8a8-104">This policy requires that Express Routes use an approved SKU.</span><span class="sxs-lookup"><span data-stu-id="ef8a8-104">This policy requires that Express Routes use an approved SKU.</span></span> <span data-ttu-id="ef8a8-105">You specify an array of allowed SKUs.</span><span class="sxs-lookup"><span data-stu-id="ef8a8-105">You specify an array of allowed SKUs.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-template"></a><span data-ttu-id="ef8a8-106">Sample template</span><span class="sxs-lookup"><span data-stu-id="ef8a8-106">Sample template</span></span>

[!code-json[main](../../../policy-templates/samples/Network/express-route-skus/azurepolicy.json "Allowed Express Route SKUs")]

<span data-ttu-id="ef8a8-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ef8a8-107">You can deploy this template using the [Azure portal](#deploy-with-the-portal), with [PowerShell](#deploy-with-powershell) or with the [Azure CLI](#deploy-with-azure-cli).</span></span>

## <a name="deploy-with-the-portal"></a><span data-ttu-id="ef8a8-108">Deploy with the portal</span><span class="sxs-lookup"><span data-stu-id="ef8a8-108">Deploy with the portal</span></span>

<span data-ttu-id="ef8a8-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fexpress-route-skus%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="ef8a8-109">[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?feature.customportal=false&microsoft_azure_policy=true&microsoft_azure_policy_policyinsights=true&feature.microsoft_azure_security_policy=true&microsoft_azure_marketplace_policy=true#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FNetwork%2Fexpress-route-skus%2Fazurepolicy.json)</span></span>

## <a name="deploy-with-powershell"></a><span data-ttu-id="ef8a8-110">Deploy with PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef8a8-110">Deploy with PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

```powershell
$definition = New-AzureRmPolicyDefinition -Name "express-route-skus" -DisplayName "Allowed Express Route SKUs" -description "This policy enables you to specify a set of express route SKUs that your organization can deploy." -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/express-route-skus/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/express-route-skus/azurepolicy.parameters.json' -Mode All
$definition
$assignment = New-AzureRMPolicyAssignment -Name <assignmentname> -Scope <scope>  -listOfAllowedSKUs <Allowed SKUs> -PolicyDefinition $definition
$assignment
```

### <a name="clean-up-powershell-deployment"></a><span data-ttu-id="ef8a8-111">Clean up PowerShell deployment</span><span class="sxs-lookup"><span data-stu-id="ef8a8-111">Clean up PowerShell deployment</span></span>

<span data-ttu-id="ef8a8-112">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ef8a8-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="deploy-with-azure-cli"></a><span data-ttu-id="ef8a8-113">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ef8a8-113">Deploy with Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

```azurecli-interactive
az policy definition create --name 'express-route-skus' --display-name 'Allowed Express Route SKUs' --description 'This policy enables you to specify a set of express route SKUs that your organization can deploy.' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/express-route-skus/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Network/express-route-skus/azurepolicy.parameters.json' --mode All

az policy assignment create --name <assignmentname> --scope <scope> --policy "express-route-skus"
```

### <a name="clean-up-azure-cli-deployment"></a><span data-ttu-id="ef8a8-114">Clean up Azure CLI deployment</span><span class="sxs-lookup"><span data-stu-id="ef8a8-114">Clean up Azure CLI deployment</span></span>

<span data-ttu-id="ef8a8-115">Run the following command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ef8a8-115">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a><span data-ttu-id="ef8a8-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="ef8a8-116">Next steps</span></span>

- <span data-ttu-id="ef8a8-117">Review more examples at [Azure Policy samples](../json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ef8a8-117">Review more examples at [Azure Policy samples](../json-samples.md).</span></span>