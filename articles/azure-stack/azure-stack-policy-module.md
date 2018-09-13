---
title: Use the Azure Stack Policy Module| Microsoft Docs
description: Learn how to constrain an Azure subscription to behave like an Azure Stack subscription
services: azure-stack
documentationcenter: ''
author: HeathL17
manager: byronr
editor: ''
ms.assetid: 937ef34f-14d4-4ea9-960b-362ba986f000
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/9/2017
ms.author: helaw
ms.openlocfilehash: 79c4011473aead13b18ae1ec24575a0bf2c59c1d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554117"
---
# <a name="manage-azure-policy-using-the-azure-stack-policy-module"></a><span data-ttu-id="9bf77-103">Manage Azure policy using the Azure Stack Policy Module</span><span class="sxs-lookup"><span data-stu-id="9bf77-103">Manage Azure policy using the Azure Stack Policy Module</span></span>
<span data-ttu-id="9bf77-104">The Azure Stack Policy module allows you to configure an Azure subscription with the same versioning and service availability as Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9bf77-104">The Azure Stack Policy module allows you to configure an Azure subscription with the same versioning and service availability as Azure Stack.</span></span>  <span data-ttu-id="9bf77-105">The module uses the **New-AzureRMPolicyAssignment** cmdlet to create an Azure policy, which limits the resource types and services available in a subscription.</span><span class="sxs-lookup"><span data-stu-id="9bf77-105">The module uses the **New-AzureRMPolicyAssignment** cmdlet to create an Azure policy, which limits the resource types and services available in a subscription.</span></span>  <span data-ttu-id="9bf77-106">Once complete, you can use your Azure subscription to develop apps for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="9bf77-106">Once complete, you can use your Azure subscription to develop apps for Azure Stack.</span></span>  

## <a name="install-the-module"></a><span data-ttu-id="9bf77-107">Install the module</span><span class="sxs-lookup"><span data-stu-id="9bf77-107">Install the module</span></span>
1. <span data-ttu-id="9bf77-108">Install the required version of the AzureRM PowerShell module, as described in Step1 of [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="9bf77-108">Install the required version of the AzureRM PowerShell module, as described in Step1 of [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>   
2. [<span data-ttu-id="9bf77-109">Download the Azure Stack tools from GitHub</span><span class="sxs-lookup"><span data-stu-id="9bf77-109">Download the Azure Stack tools from GitHub</span></span>](azure-stack-powershell-download.md)  
3. [<span data-ttu-id="9bf77-110">Configure PowerShell for use with Azure Stack</span><span class="sxs-lookup"><span data-stu-id="9bf77-110">Configure PowerShell for use with Azure Stack</span></span>](azure-stack-powershell-configure.md)

4. <span data-ttu-id="9bf77-111">Import the AzureStack.Policy.psm1 module:</span><span class="sxs-lookup"><span data-stu-id="9bf77-111">Import the AzureStack.Policy.psm1 module:</span></span>

   ```PowerShell
   import-module .\Policy\AzureStack.Policy.psm1
   ```

## <a name="apply-policy-to-subscription"></a><span data-ttu-id="9bf77-112">Apply policy to subscription</span><span class="sxs-lookup"><span data-stu-id="9bf77-112">Apply policy to subscription</span></span>
<span data-ttu-id="9bf77-113">The following command can be used to apply a default Azure Stack policy against your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9bf77-113">The following command can be used to apply a default Azure Stack policy against your Azure subscription.</span></span> <span data-ttu-id="9bf77-114">Before running, replace *Azure Subscription Name* with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9bf77-114">Before running, replace *Azure Subscription Name* with your Azure subscription.</span></span>

```PowerShell
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
$rgName = 'AzureStack'
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID

```

## <a name="apply-policy-to-a-resource-group"></a><span data-ttu-id="9bf77-115">Apply policy to a resource group</span><span class="sxs-lookup"><span data-stu-id="9bf77-115">Apply policy to a resource group</span></span>
<span data-ttu-id="9bf77-116">You may want to apply policies in a more granular method.</span><span class="sxs-lookup"><span data-stu-id="9bf77-116">You may want to apply policies in a more granular method.</span></span>  <span data-ttu-id="9bf77-117">As an example, you may have other resources running in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="9bf77-117">As an example, you may have other resources running in the same subscription.</span></span>  <span data-ttu-id="9bf77-118">You can scope the policy application to a specific resource group, which lets you test your apps for Azure Stack using Azure resources.</span><span class="sxs-lookup"><span data-stu-id="9bf77-118">You can scope the policy application to a specific resource group, which lets you test your apps for Azure Stack using Azure resources.</span></span> <span data-ttu-id="9bf77-119">Before running, replace *Azure Subscription Name* with your Azure subscription name.</span><span class="sxs-lookup"><span data-stu-id="9bf77-119">Before running, replace *Azure Subscription Name* with your Azure subscription name.</span></span>

```PowerShell
$resourceGroupName = ‘myRG01’
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzureStackRmPolicy)
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID/resourceGroups/$rgName

```

## <a name="policy-in-action"></a><span data-ttu-id="9bf77-120">Policy in action</span><span class="sxs-lookup"><span data-stu-id="9bf77-120">Policy in action</span></span>
<span data-ttu-id="9bf77-121">Once you've deployed the Azure policy, you receive an error when you try to deploy a resource that prohibited by policy.</span><span class="sxs-lookup"><span data-stu-id="9bf77-121">Once you've deployed the Azure policy, you receive an error when you try to deploy a resource that prohibited by policy.</span></span>  

![Result of resource deployment failure because of policy constraint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-policy-module/image1.png)

## <a name="next-steps"></a><span data-ttu-id="9bf77-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="9bf77-123">Next steps</span></span>
[<span data-ttu-id="9bf77-124">Deploy templates with PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bf77-124">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)

[<span data-ttu-id="9bf77-125">Deploy templates with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9bf77-125">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)

[<span data-ttu-id="9bf77-126">Deploy Templates with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9bf77-126">Deploy Templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

