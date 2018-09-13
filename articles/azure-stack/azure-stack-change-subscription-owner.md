---
title: Update the owner of Azure Stack user subscription | Microsoft Docs
description: Change the Billing Owner for Azure STack user subscriptions.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: get-started-article
ms.date: 06/12/2018
ms.author: brenduns
ms.reviewer: shnatara
ms.openlocfilehash: de8610944e11d8cf106ac484a0c6634c8661b5a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868312"
---
# <a name="change-the-owner-for-an-azure-stack-user-subscription"></a><span data-ttu-id="97f0e-103">Change the Owner for an Azure Stack user subscription</span><span class="sxs-lookup"><span data-stu-id="97f0e-103">Change the Owner for an Azure Stack user subscription</span></span>

<span data-ttu-id="97f0e-104">Azure Stack operators can use PowerShell to change the Billing Owner of a user subscription.</span><span class="sxs-lookup"><span data-stu-id="97f0e-104">Azure Stack operators can use PowerShell to change the Billing Owner of a user subscription.</span></span> <span data-ttu-id="97f0e-105">One reason to change the owner is to replace a user that leaves your organization.</span><span class="sxs-lookup"><span data-stu-id="97f0e-105">One reason to change the owner is to replace a user that leaves your organization.</span></span>   

<span data-ttu-id="97f0e-106">There are two types of *Owners* that are assigned to a subscription:</span><span class="sxs-lookup"><span data-stu-id="97f0e-106">There are two types of *Owners* that are assigned to a subscription:</span></span>

- <span data-ttu-id="97f0e-107">**Billing Owner** – By default, the Billing Owner is the user account that gets the subscription from an Offer and then owns the billing relationship for that subscription.</span><span class="sxs-lookup"><span data-stu-id="97f0e-107">**Billing Owner** – By default, the Billing Owner is the user account that gets the subscription from an Offer and then owns the billing relationship for that subscription.</span></span> <span data-ttu-id="97f0e-108">This account is also an administrator of the subscription.</span><span class="sxs-lookup"><span data-stu-id="97f0e-108">This account is also an administrator of the subscription.</span></span>  <span data-ttu-id="97f0e-109">Only one user account can have this designation on a subscription.</span><span class="sxs-lookup"><span data-stu-id="97f0e-109">Only one user account can have this designation on a subscription.</span></span> <span data-ttu-id="97f0e-110">A Billing Owner is often an organization or team lead.</span><span class="sxs-lookup"><span data-stu-id="97f0e-110">A Billing Owner is often an organization or team lead.</span></span> 

  <span data-ttu-id="97f0e-111">You use the PowerShell cmdlet the **Set-AzsUserSubscription** to change the Billing Owner.</span><span class="sxs-lookup"><span data-stu-id="97f0e-111">You use the PowerShell cmdlet the **Set-AzsUserSubscription** to change the Billing Owner.</span></span>  

- <span data-ttu-id="97f0e-112">**Owners added through RBAC roles** – Additional users can be granted the Owner role using the [Role Based Access Control](azure-stack-manage-permissions.md) (RBAC) system.</span><span class="sxs-lookup"><span data-stu-id="97f0e-112">**Owners added through RBAC roles** – Additional users can be granted the Owner role using the [Role Based Access Control](azure-stack-manage-permissions.md) (RBAC) system.</span></span>  <span data-ttu-id="97f0e-113">Any number of additional user accounts can be added as owners to compliment the Billing Owner.</span><span class="sxs-lookup"><span data-stu-id="97f0e-113">Any number of additional user accounts can be added as owners to compliment the Billing Owner.</span></span> <span data-ttu-id="97f0e-114">Additional owners are also administrators of the subscription and have all privileges for the subscription except permissions to delete the Billing  Owner.</span><span class="sxs-lookup"><span data-stu-id="97f0e-114">Additional owners are also administrators of the subscription and have all privileges for the subscription except permissions to delete the Billing  Owner.</span></span> 

  <span data-ttu-id="97f0e-115">You can use PowerShell to manage additional owners, see [Azure PowerShell to manage role-based access control]( https://docs.microsoft.com/azure/role-based-access-control/role-assignments-powershell).</span><span class="sxs-lookup"><span data-stu-id="97f0e-115">You can use PowerShell to manage additional owners, see [Azure PowerShell to manage role-based access control]( https://docs.microsoft.com/azure/role-based-access-control/role-assignments-powershell).</span></span>


## <a name="change-the-billing-owner"></a><span data-ttu-id="97f0e-116">Change the Billing Owner</span><span class="sxs-lookup"><span data-stu-id="97f0e-116">Change the Billing Owner</span></span>
<span data-ttu-id="97f0e-117">Run the following script to change the Billing Owner of a user subscription.</span><span class="sxs-lookup"><span data-stu-id="97f0e-117">Run the following script to change the Billing Owner of a user subscription.</span></span>  <span data-ttu-id="97f0e-118">The computer that you use to run the script must connect to Azure Stack and run the Azure Stack PowerShell module 1.3.0 or later.</span><span class="sxs-lookup"><span data-stu-id="97f0e-118">The computer that you use to run the script must connect to Azure Stack and run the Azure Stack PowerShell module 1.3.0 or later.</span></span> <span data-ttu-id="97f0e-119">For more information, see [Install Azure Stack PowerShell](azure-stack-powershell-install.md).</span><span class="sxs-lookup"><span data-stu-id="97f0e-119">For more information, see [Install Azure Stack PowerShell](azure-stack-powershell-install.md).</span></span> 

> [!Note]  
>  <span data-ttu-id="97f0e-120">In a multi-tenanted Azure Stack, the new owner must be in the same directory as the existing owner.</span><span class="sxs-lookup"><span data-stu-id="97f0e-120">In a multi-tenanted Azure Stack, the new owner must be in the same directory as the existing owner.</span></span> <span data-ttu-id="97f0e-121">Before you can provide ownership of the subscription to a user that is in another directory, you must first [invite that user as a guest into your Directory](https://docs.microsoft.com/azure/active-directory/b2b/add-users-administrator).</span><span class="sxs-lookup"><span data-stu-id="97f0e-121">Before you can provide ownership of the subscription to a user that is in another directory, you must first [invite that user as a guest into your Directory](https://docs.microsoft.com/azure/active-directory/b2b/add-users-administrator).</span></span> 


<span data-ttu-id="97f0e-122">Replace the following values in the script before it runs:</span><span class="sxs-lookup"><span data-stu-id="97f0e-122">Replace the following values in the script before it runs:</span></span> 
 
- <span data-ttu-id="97f0e-123">**$ArmEndpoint** –  Specify the Resource Manager endpoint for your environment.</span><span class="sxs-lookup"><span data-stu-id="97f0e-123">**$ArmEndpoint** –  Specify the Resource Manager endpoint for your environment.</span></span>  
- <span data-ttu-id="97f0e-124">**$TenantId**   - Specify your Tenant ID.</span><span class="sxs-lookup"><span data-stu-id="97f0e-124">**$TenantId**   - Specify your Tenant ID.</span></span> 
- <span data-ttu-id="97f0e-125">**$SubscriptionId** – Specify your Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="97f0e-125">**$SubscriptionId** – Specify your Subscription ID.</span></span>
- <span data-ttu-id="97f0e-126">**$OwnerUpn** - Specify an account as *user@example.com* to  add as the new Billing Owner.</span><span class="sxs-lookup"><span data-stu-id="97f0e-126">**$OwnerUpn** - Specify an account as *user@example.com* to  add as the new Billing Owner.</span></span>  


```PowerSHell   
# Setup Azure Stack Admin Environment
Add-AzureRmEnvironment -ARMEndpoint $ArmEndpoint -Name AzureStack-admin
Add-AzureRmAccount -Environment AzureStack-admin -TenantId $TenantId

# Select Admin Subscriptionr
$providerSubscriptionId = (Get-AzureRmSubscription -SubscriptionName "Default Provider Subscription").Id
Write-Output "Setting context the Default Provider Subscription: $providerSubscriptionId" 
Set-AzureRmContext -Subscription $providerSubscriptionId

# Change User Subscription owner
$subscription = Get-AzsUserSubscription -SubscriptionId $SubscriptionId
$Subscription.Owner = $OwnerUpn
Set-AzsUserSubscription -InputObject $subscription
```


## <a name="next-steps"></a><span data-ttu-id="97f0e-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="97f0e-127">Next steps</span></span>
[<span data-ttu-id="97f0e-128">Manage Role-Based Access Control</span><span class="sxs-lookup"><span data-stu-id="97f0e-128">Manage Role-Based Access Control</span></span>](azure-stack-manage-permissions.md)
