---
title: Create an offer in Azure Stack | Microsoft Docs
description: As a cloud administrator, learn how to create an offer for your users in Azure Stack.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/20/2018
ms.author: brenduns
ms.reviewer: efemmano
ms.openlocfilehash: 66a89c3cb14dd642ae993cbf3c45885635f59759
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44793473"
---
# <a name="create-an-offer-in-azure-stack"></a><span data-ttu-id="1549e-103">Create an offer in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="1549e-103">Create an offer in Azure Stack</span></span>

<span data-ttu-id="1549e-104">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present to users to buy or subscribe to.</span><span class="sxs-lookup"><span data-stu-id="1549e-104">[Offers](azure-stack-key-features.md) are groups of one or more plans that providers present to users to buy or subscribe to.</span></span> <span data-ttu-id="1549e-105">This document shows you how to create an offer that includes the [plan that you created](azure-stack-create-plan.md).</span><span class="sxs-lookup"><span data-stu-id="1549e-105">This document shows you how to create an offer that includes the [plan that you created](azure-stack-create-plan.md).</span></span> <span data-ttu-id="1549e-106">This offer gives subscribers the ability to set up virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1549e-106">This offer gives subscribers the ability to set up virtual machines.</span></span>

1. <span data-ttu-id="1549e-107">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external) and select **New** > **Tenant Offers + Plans** > **Offer**.</span><span class="sxs-lookup"><span data-stu-id="1549e-107">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external) and select **New** > **Tenant Offers + Plans** > **Offer**.</span></span>

   ![Create an offer](media/azure-stack-create-offer/image01.png)
  
2. <span data-ttu-id="1549e-109">Under **New Offer**, enter a **Display Name** and a **Resource Name**, and then under **Resource Group**, select **Create new** or **Use existing**.</span><span class="sxs-lookup"><span data-stu-id="1549e-109">Under **New Offer**, enter a **Display Name** and a **Resource Name**, and then under **Resource Group**, select **Create new** or **Use existing**.</span></span> <span data-ttu-id="1549e-110">The Display Name is the friendly name for the offer.</span><span class="sxs-lookup"><span data-stu-id="1549e-110">The Display Name is the friendly name for the offer.</span></span> <span data-ttu-id="1549e-111">This friendly name is the only information about the offer that the users see when they subscribe to an offer.</span><span class="sxs-lookup"><span data-stu-id="1549e-111">This friendly name is the only information about the offer that the users see when they subscribe to an offer.</span></span> <span data-ttu-id="1549e-112">Use an intuitive name that helps users understand what comes with the offer.</span><span class="sxs-lookup"><span data-stu-id="1549e-112">Use an intuitive name that helps users understand what comes with the offer.</span></span> <span data-ttu-id="1549e-113">Only the admin can see the Resource Name.</span><span class="sxs-lookup"><span data-stu-id="1549e-113">Only the admin can see the Resource Name.</span></span> <span data-ttu-id="1549e-114">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span><span class="sxs-lookup"><span data-stu-id="1549e-114">It's the name that admins use to work with the offer as an Azure Resource Manager resource.</span></span>

   ![New Offer](media/azure-stack-create-offer/image01a.png)
  
3. <span data-ttu-id="1549e-116">Select **Base plans** to open the **Plan**.</span><span class="sxs-lookup"><span data-stu-id="1549e-116">Select **Base plans** to open the **Plan**.</span></span> <span data-ttu-id="1549e-117">Select the plans you want to include in the offer, and then choose **Select**.</span><span class="sxs-lookup"><span data-stu-id="1549e-117">Select the plans you want to include in the offer, and then choose **Select**.</span></span> <span data-ttu-id="1549e-118">To create the offer select **Create**.</span><span class="sxs-lookup"><span data-stu-id="1549e-118">To create the offer select **Create**.</span></span>

   ![Select plan](media/azure-stack-create-offer/image02.png)
  
4. <span data-ttu-id="1549e-120">After creating the offer, you can change its state.</span><span class="sxs-lookup"><span data-stu-id="1549e-120">After creating the offer, you can change its state.</span></span> <span data-ttu-id="1549e-121">Offers must be made *public* for users to get the full view when they subscribe.</span><span class="sxs-lookup"><span data-stu-id="1549e-121">Offers must be made *public* for users to get the full view when they subscribe.</span></span> <span data-ttu-id="1549e-122">Offers can be:</span><span class="sxs-lookup"><span data-stu-id="1549e-122">Offers can be:</span></span>

   - <span data-ttu-id="1549e-123">**Public**: Visible to users.</span><span class="sxs-lookup"><span data-stu-id="1549e-123">**Public**: Visible to users.</span></span>
   - <span data-ttu-id="1549e-124">**Private**: Only visible to cloud administrators.</span><span class="sxs-lookup"><span data-stu-id="1549e-124">**Private**: Only visible to cloud administrators.</span></span> <span data-ttu-id="1549e-125">This setting is useful while drafting the plan or offer, or if the cloud administrator wants to [create each subscription for users](azure-stack-subscribe-plan-provision-vm.md#create-a-subscription-as-a-cloud-operator).</span><span class="sxs-lookup"><span data-stu-id="1549e-125">This setting is useful while drafting the plan or offer, or if the cloud administrator wants to [create each subscription for users](azure-stack-subscribe-plan-provision-vm.md#create-a-subscription-as-a-cloud-operator).</span></span>
   - <span data-ttu-id="1549e-126">**Decommissioned**: Closed to new subscribers.</span><span class="sxs-lookup"><span data-stu-id="1549e-126">**Decommissioned**: Closed to new subscribers.</span></span> <span data-ttu-id="1549e-127">The cloud administrator can use decommissioned to prevent future subscriptions, but leave current subscribers unaffected.</span><span class="sxs-lookup"><span data-stu-id="1549e-127">The cloud administrator can use decommissioned to prevent future subscriptions, but leave current subscribers unaffected.</span></span>

   > [!TIP]  
   > <span data-ttu-id="1549e-128">Changes to the offer aren't immediately visible to user.</span><span class="sxs-lookup"><span data-stu-id="1549e-128">Changes to the offer aren't immediately visible to user.</span></span> <span data-ttu-id="1549e-129">To see the changes, users might have to sign out and sign in again to the user portal to see the new offer.</span><span class="sxs-lookup"><span data-stu-id="1549e-129">To see the changes, users might have to sign out and sign in again to the user portal to see the new offer.</span></span>

   <span data-ttu-id="1549e-130">On the Overview for the offer, select **Accessibility state**.</span><span class="sxs-lookup"><span data-stu-id="1549e-130">On the Overview for the offer, select **Accessibility state**.</span></span> <span data-ttu-id="1549e-131">Choose the state you want to use (for example, **Public**) and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="1549e-131">Choose the state you want to use (for example, **Public**) and then select **Save**.</span></span>
 
     ![Choose the state](media/azure-stack-create-offer/change-stage-1807.png)

     <span data-ttu-id="1549e-133">As an alternative, select **Change state** and then choose a state.</span><span class="sxs-lookup"><span data-stu-id="1549e-133">As an alternative, select **Change state** and then choose a state.</span></span>

    ![Select Accessibility state](media/azure-stack-create-offer/change-stage-select-1807.png)

   > [!NOTE]
   > <span data-ttu-id="1549e-135">You can also use PowerShell to create default offers, plans, and quotas.</span><span class="sxs-lookup"><span data-stu-id="1549e-135">You can also use PowerShell to create default offers, plans, and quotas.</span></span> <span data-ttu-id="1549e-136">For more information, see [Azure Stack PowerShell Module 1.4.0](https://docs.microsoft.com/powershell/azure/azure-stack/overview?view=azurestackps-1.4.0).</span><span class="sxs-lookup"><span data-stu-id="1549e-136">For more information, see [Azure Stack PowerShell Module 1.4.0](https://docs.microsoft.com/powershell/azure/azure-stack/overview?view=azurestackps-1.4.0).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1549e-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="1549e-137">Next steps</span></span>

- [<span data-ttu-id="1549e-138">Create subscriptions</span><span class="sxs-lookup"><span data-stu-id="1549e-138">Create subscriptions</span></span>](azure-stack-subscribe-plan-provision-vm.md)
- [<span data-ttu-id="1549e-139">Provision a virtual machine</span><span class="sxs-lookup"><span data-stu-id="1549e-139">Provision a virtual machine</span></span>](azure-stack-provision-vm.md)
