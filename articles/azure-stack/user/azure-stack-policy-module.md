---
title: Use the Azure Stack Policy Module| Microsoft Docs
description: Learn how to constrain an Azure subscription to behave like an Azure Stack subscription
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: 937ef34f-14d4-4ea9-960b-362ba986f000
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: sethm
ms.openlocfilehash: 273b1065d51552dd7b92d4a10fc856294a23a4e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865919"
---
# <a name="manage-azure-policy-using-the-azure-stack-policy-module"></a><span data-ttu-id="09705-103">Manage Azure policy using the Azure Stack Policy Module</span><span class="sxs-lookup"><span data-stu-id="09705-103">Manage Azure policy using the Azure Stack Policy Module</span></span>

<span data-ttu-id="09705-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="09705-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="09705-105">The Azure Stack Policy module allows you to configure an Azure subscription with the same versioning and service availability as Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="09705-105">The Azure Stack Policy module allows you to configure an Azure subscription with the same versioning and service availability as Azure Stack.</span></span>  <span data-ttu-id="09705-106">The module uses the **New-AzureRMPolicyAssignment** cmdlet to create an Azure policy, which limits the resource types and services available in a subscription.</span><span class="sxs-lookup"><span data-stu-id="09705-106">The module uses the **New-AzureRMPolicyAssignment** cmdlet to create an Azure policy, which limits the resource types and services available in a subscription.</span></span>  <span data-ttu-id="09705-107">After configuring the policy, you can use your Azure subscription to develop apps targeted for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="09705-107">After configuring the policy, you can use your Azure subscription to develop apps targeted for Azure Stack.</span></span>

## <a name="install-the-module"></a><span data-ttu-id="09705-108">Install the module</span><span class="sxs-lookup"><span data-stu-id="09705-108">Install the module</span></span>

1. <span data-ttu-id="09705-109">Install the required version of the AzureRM PowerShell module, as described in Step1 of [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="09705-109">Install the required version of the AzureRM PowerShell module, as described in Step1 of [Install PowerShell for Azure Stack](azure-stack-powershell-install.md).</span></span>
2. [<span data-ttu-id="09705-110">Download the Azure Stack tools from GitHub</span><span class="sxs-lookup"><span data-stu-id="09705-110">Download the Azure Stack tools from GitHub</span></span>](azure-stack-powershell-download.md)
3. [<span data-ttu-id="09705-111">Configure PowerShell for use with Azure Stack</span><span class="sxs-lookup"><span data-stu-id="09705-111">Configure PowerShell for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md)

4. <span data-ttu-id="09705-112">Import the AzureStack.Policy.psm1 module:</span><span class="sxs-lookup"><span data-stu-id="09705-112">Import the AzureStack.Policy.psm1 module:</span></span>

   ```PowerShell
   Import-Module .\Policy\AzureStack.Policy.psm1
   ```

## <a name="apply-policy-to-azure-subscription"></a><span data-ttu-id="09705-113">Apply policy to Azure subscription</span><span class="sxs-lookup"><span data-stu-id="09705-113">Apply policy to Azure subscription</span></span>

<span data-ttu-id="09705-114">You can use the following command to apply a default Azure Stack policy against your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="09705-114">You can use the following command to apply a default Azure Stack policy against your Azure subscription.</span></span> <span data-ttu-id="09705-115">Before running this command, replace *Azure Subscription Name* with your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="09705-115">Before running this command, replace *Azure Subscription Name* with your Azure subscription.</span></span>

```PowerShell
Add-AzureRmAccount
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzsPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID

```

## <a name="apply-policy-to-a-resource-group"></a><span data-ttu-id="09705-116">Apply policy to a resource group</span><span class="sxs-lookup"><span data-stu-id="09705-116">Apply policy to a resource group</span></span>

<span data-ttu-id="09705-117">You may want to apply policies that are more granular.</span><span class="sxs-lookup"><span data-stu-id="09705-117">You may want to apply policies that are more granular.</span></span> <span data-ttu-id="09705-118">As an example, you might have other resources running in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="09705-118">As an example, you might have other resources running in the same subscription.</span></span> <span data-ttu-id="09705-119">You can scope the policy application to a specific resource group, which lets you test your apps for Azure Stack using Azure resources.</span><span class="sxs-lookup"><span data-stu-id="09705-119">You can scope the policy application to a specific resource group, which lets you test your apps for Azure Stack using Azure resources.</span></span> <span data-ttu-id="09705-120">Before running the following command, replace *Azure Subscription Name* with your Azure subscription name.</span><span class="sxs-lookup"><span data-stu-id="09705-120">Before running the following command, replace *Azure Subscription Name* with your Azure subscription name.</span></span>

```PowerShell
Add-AzureRmAccount
$rgName = 'myRG01'
$s = Select-AzureRmSubscription -SubscriptionName "<Azure Subscription Name>"
$policy = New-AzureRmPolicyDefinition -Name AzureStackPolicyDefinition -Policy (Get-AzsPolicy)
$subscriptionID = $s.Subscription.SubscriptionId
New-AzureRmPolicyAssignment -Name AzureStack -PolicyDefinition $policy -Scope /subscriptions/$subscriptionID/resourceGroups/$rgName

```

## <a name="policy-in-action"></a><span data-ttu-id="09705-121">Policy in action</span><span class="sxs-lookup"><span data-stu-id="09705-121">Policy in action</span></span>

<span data-ttu-id="09705-122">Once you've deployed the Azure policy, you receive an error when you try to deploy a resource that prohibited by policy.</span><span class="sxs-lookup"><span data-stu-id="09705-122">Once you've deployed the Azure policy, you receive an error when you try to deploy a resource that prohibited by policy.</span></span>

![Result of resource deployment failure because of policy constraint](./media/azure-stack-policy-module/image1.png)

## <a name="next-steps"></a><span data-ttu-id="09705-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="09705-124">Next steps</span></span>

* [<span data-ttu-id="09705-125">Deploy templates with PowerShell</span><span class="sxs-lookup"><span data-stu-id="09705-125">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
* [<span data-ttu-id="09705-126">Deploy templates with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="09705-126">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)
* [<span data-ttu-id="09705-127">Deploy Templates with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09705-127">Deploy Templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)
