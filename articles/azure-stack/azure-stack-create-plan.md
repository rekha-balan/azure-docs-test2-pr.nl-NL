---
title: Create a plan in Azure Stack | Microsoft Docs
description: As a cloud administrator, create a plan that lets subscribers provision virtual machines.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: 3dc92e5c-c004-49db-9a94-783f1f798b98
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/07/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: 1fa01d23108ce92fbd7c854442c0474b19395d25
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44821475"
---
# <a name="create-a-plan-in-azure-stack"></a><span data-ttu-id="3a276-103">Create a plan in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3a276-103">Create a plan in Azure Stack</span></span>

<span data-ttu-id="3a276-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="3a276-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="3a276-105">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span><span class="sxs-lookup"><span data-stu-id="3a276-105">[Plans](azure-stack-key-features.md) are groupings of one or more services.</span></span> <span data-ttu-id="3a276-106">As a provider, you can create plans to offer to your users.</span><span class="sxs-lookup"><span data-stu-id="3a276-106">As a provider, you can create plans to offer to your users.</span></span> <span data-ttu-id="3a276-107">In turn, your users subscribe to your offers to use the plans and services they include.</span><span class="sxs-lookup"><span data-stu-id="3a276-107">In turn, your users subscribe to your offers to use the plans and services they include.</span></span> <span data-ttu-id="3a276-108">This example shows you how to create a plan that includes the compute, network, and storage resource providers.</span><span class="sxs-lookup"><span data-stu-id="3a276-108">This example shows you how to create a plan that includes the compute, network, and storage resource providers.</span></span> <span data-ttu-id="3a276-109">This plan gives subscribers the ability to provision virtual machines.</span><span class="sxs-lookup"><span data-stu-id="3a276-109">This plan gives subscribers the ability to provision virtual machines.</span></span>

1. <span data-ttu-id="3a276-110">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="3a276-110">Sign in to the Azure Stack administrator portal (https://adminportal.local.azurestack.external).</span></span>

2. <span data-ttu-id="3a276-111">To create a plan and offer that users can subscribe to, select **New** > **Offers + Plans** > **Plan**.</span><span class="sxs-lookup"><span data-stu-id="3a276-111">To create a plan and offer that users can subscribe to, select **New** > **Offers + Plans** > **Plan**.</span></span>
  
   ![Select a plan](media/azure-stack-create-plan/select-plan.png)

3. <span data-ttu-id="3a276-113">Under **New plan**, enter a **Display name** and a **Resource name**.</span><span class="sxs-lookup"><span data-stu-id="3a276-113">Under **New plan**, enter a **Display name** and a **Resource name**.</span></span> <span data-ttu-id="3a276-114">The Display name is the plan's friendly name that users can see.</span><span class="sxs-lookup"><span data-stu-id="3a276-114">The Display name is the plan's friendly name that users can see.</span></span> <span data-ttu-id="3a276-115">Only the admin can see the Resource name, which admins use to work with the plan as an Azure Resource Manager resource.</span><span class="sxs-lookup"><span data-stu-id="3a276-115">Only the admin can see the Resource name, which admins use to work with the plan as an Azure Resource Manager resource.</span></span>

   ![Specify details](media/azure-stack-create-plan/plan-name.png)

4. <span data-ttu-id="3a276-117">Create a new **Resource Group**, or select an existing one, as a container for the plan.</span><span class="sxs-lookup"><span data-stu-id="3a276-117">Create a new **Resource Group**, or select an existing one, as a container for the plan.</span></span>

   ![Specify the resource group](media/azure-stack-create-plan/resource-group.png)

5. <span data-ttu-id="3a276-119">Select **Services** and then select the checkbox for **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**.</span><span class="sxs-lookup"><span data-stu-id="3a276-119">Select **Services** and then select the checkbox for **Microsoft.Compute**, **Microsoft.Network**, and **Microsoft.Storage**.</span></span> <span data-ttu-id="3a276-120">Next, choose **Select** to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="3a276-120">Next, choose **Select** to save the configuration.</span></span> <span data-ttu-id="3a276-121">Checkboxes appear when the mouse hovers over each option.</span><span class="sxs-lookup"><span data-stu-id="3a276-121">Checkboxes appear when the mouse hovers over each option.</span></span>
  
   ![Select services](media/azure-stack-create-plan/services.png)

6. <span data-ttu-id="3a276-123">Select **Quotas**, **Microsoft.Storage (local)**, and then choose either the default quota or select **Create new quota** to create a customized quota.</span><span class="sxs-lookup"><span data-stu-id="3a276-123">Select **Quotas**, **Microsoft.Storage (local)**, and then choose either the default quota or select **Create new quota** to create a customized quota.</span></span>
  
   ![Quotas](media/azure-stack-create-plan/quotas.png)

7. <span data-ttu-id="3a276-125">If you're creating a new quota, enter a **Name** for the quota > specify the quota values > select **OK**.</span><span class="sxs-lookup"><span data-stu-id="3a276-125">If you're creating a new quota, enter a **Name** for the quota > specify the quota values > select **OK**.</span></span> <span data-ttu-id="3a276-126">The **Create quota** dialog closes.</span><span class="sxs-lookup"><span data-stu-id="3a276-126">The **Create quota** dialog closes.</span></span>

   ![New quota](media/azure-stack-create-plan/new-quota.png)

   <span data-ttu-id="3a276-128">You then select the new quota you created.</span><span class="sxs-lookup"><span data-stu-id="3a276-128">You then select the new quota you created.</span></span> <span data-ttu-id="3a276-129">Selecting the quota assigns it and closes the selection dialog.</span><span class="sxs-lookup"><span data-stu-id="3a276-129">Selecting the quota assigns it and closes the selection dialog.</span></span>
  
   ![Assign the quota](media/azure-stack-create-plan/assign-quota.png)

8. <span data-ttu-id="3a276-131">Repeat steps 6 and 7 to create and assign quotas for **Microsoft.Network (local)** and **Microsoft.Compute (local)**.</span><span class="sxs-lookup"><span data-stu-id="3a276-131">Repeat steps 6 and 7 to create and assign quotas for **Microsoft.Network (local)** and **Microsoft.Compute (local)**.</span></span> <span data-ttu-id="3a276-132">When all three services have quotas assigned, they'll look like the next example.</span><span class="sxs-lookup"><span data-stu-id="3a276-132">When all three services have quotas assigned, they'll look like the next example.</span></span>

   ![Complete quota assignments](media/azure-stack-create-plan/all-quotas-assigned.png)

9. <span data-ttu-id="3a276-134">Under **Quotas**, choose **OK**, and then under **New plan**, choose **Create** to create the plan.</span><span class="sxs-lookup"><span data-stu-id="3a276-134">Under **Quotas**, choose **OK**, and then under **New plan**, choose **Create** to create the plan.</span></span>

    ![Create the plan](media/azure-stack-create-plan/create.png)

10. <span data-ttu-id="3a276-136">To see your new plan, select **All resources**, then search for the plan and select its name.</span><span class="sxs-lookup"><span data-stu-id="3a276-136">To see your new plan, select **All resources**, then search for the plan and select its name.</span></span> <span data-ttu-id="3a276-137">If your list of resources is long, use **Search** to locate your plan by name.</span><span class="sxs-lookup"><span data-stu-id="3a276-137">If your list of resources is long, use **Search** to locate your plan by name.</span></span>

   ![Review the plan](media/azure-stack-create-plan/plan-overview.png)

## <a name="next-steps"></a><span data-ttu-id="3a276-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="3a276-139">Next steps</span></span>

[<span data-ttu-id="3a276-140">Create an offer</span><span class="sxs-lookup"><span data-stu-id="3a276-140">Create an offer</span></span>](azure-stack-create-offer.md)
