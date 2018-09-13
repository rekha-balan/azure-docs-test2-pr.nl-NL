---
title: In this article, you learn how to update Azure Stack offers and plans | Microsoft Docs
description: This article describes how to view and modify existing Azure Stack offers and plans.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.custom: mvc
ms.date: 07/30/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: a35ba993e6fd1162fa4a18bc0d6bc9351fe7dfa2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868642"
---
# <a name="azure-stack-add-on-plans"></a><span data-ttu-id="98617-103">Azure Stack add-on plans</span><span class="sxs-lookup"><span data-stu-id="98617-103">Azure Stack add-on plans</span></span>

<span data-ttu-id="98617-104">As an Azure Stack operator, you create add-on plans to modify a [*base plan*](azure-stack-create-plan.md) when you want to offer additional services or extend *computer*, *storage*, or *network* quotas beyond the base plans initial offer.</span><span class="sxs-lookup"><span data-stu-id="98617-104">As an Azure Stack operator, you create add-on plans to modify a [*base plan*](azure-stack-create-plan.md) when you want to offer additional services or extend *computer*, *storage*, or *network* quotas beyond the base plans initial offer.</span></span> <span data-ttu-id="98617-105">Add-on plans modify the base plan and are optional extensions that users can choose to subscribe to.</span><span class="sxs-lookup"><span data-stu-id="98617-105">Add-on plans modify the base plan and are optional extensions that users can choose to subscribe to.</span></span> 

<span data-ttu-id="98617-106">There are times when combining everything in a single plan is optimal.</span><span class="sxs-lookup"><span data-stu-id="98617-106">There are times when combining everything in a single plan is optimal.</span></span> <span data-ttu-id="98617-107">Other times you might want to have a base plan and then offer the additional services by using add-on plans.</span><span class="sxs-lookup"><span data-stu-id="98617-107">Other times you might want to have a base plan and then offer the additional services by using add-on plans.</span></span> <span data-ttu-id="98617-108">For instance, you could decide to offer IaaS services as part of a base plan, with all PaaS services treated as add-on plans.</span><span class="sxs-lookup"><span data-stu-id="98617-108">For instance, you could decide to offer IaaS services as part of a base plan, with all PaaS services treated as add-on plans.</span></span>

<span data-ttu-id="98617-109">Another reason to use add-on plans is to help users be mindful of their resource usage.</span><span class="sxs-lookup"><span data-stu-id="98617-109">Another reason to use add-on plans is to help users be mindful of their resource usage.</span></span> <span data-ttu-id="98617-110">To do so, you could start with a base plan that includes relatively small quotas (depending on the services required).</span><span class="sxs-lookup"><span data-stu-id="98617-110">To do so, you could start with a base plan that includes relatively small quotas (depending on the services required).</span></span> <span data-ttu-id="98617-111">Then, as users reach capacity, they would be alerted that they've consumed the allocation of resources based on their assigned plan.</span><span class="sxs-lookup"><span data-stu-id="98617-111">Then, as users reach capacity, they would be alerted that they've consumed the allocation of resources based on their assigned plan.</span></span> <span data-ttu-id="98617-112">From there, the users could then select an add-on plan that provides the additional resources.</span><span class="sxs-lookup"><span data-stu-id="98617-112">From there, the users could then select an add-on plan that provides the additional resources.</span></span>

> [!NOTE]
> <span data-ttu-id="98617-113">When you don’t want to use an add-on plan to extend a quota, you can also choose to [edit the original configuration of the quota](azure-stack-quota-types.md#to-edit-a-quota).</span><span class="sxs-lookup"><span data-stu-id="98617-113">When you don’t want to use an add-on plan to extend a quota, you can also choose to [edit the original configuration of the quota](azure-stack-quota-types.md#to-edit-a-quota).</span></span> 

<span data-ttu-id="98617-114">When a user adds an add-on plan to an existing offer subscription, the additional resources could take up to an hour to appear.</span><span class="sxs-lookup"><span data-stu-id="98617-114">When a user adds an add-on plan to an existing offer subscription, the additional resources could take up to an hour to appear.</span></span> 

## <a name="create-an-add-on-plan"></a><span data-ttu-id="98617-115">Create an add-on plan</span><span class="sxs-lookup"><span data-stu-id="98617-115">Create an add-on plan</span></span>
<span data-ttu-id="98617-116">Add-on plans are created by modifying an existing offer:</span><span class="sxs-lookup"><span data-stu-id="98617-116">Add-on plans are created by modifying an existing offer:</span></span>

1. <span data-ttu-id="98617-117">Sign in to the Azure Stack administrator portal as a cloud administrator.</span><span class="sxs-lookup"><span data-stu-id="98617-117">Sign in to the Azure Stack administrator portal as a cloud administrator.</span></span>
2. <span data-ttu-id="98617-118">Follow the same steps used to [create a new base plan](azure-stack-create-plan.md) to create a new plan offering services that were not previously offered.</span><span class="sxs-lookup"><span data-stu-id="98617-118">Follow the same steps used to [create a new base plan](azure-stack-create-plan.md) to create a new plan offering services that were not previously offered.</span></span> <span data-ttu-id="98617-119">In this example, Key Vault (Microsoft.KeyVault) services will be included in the new plan.</span><span class="sxs-lookup"><span data-stu-id="98617-119">In this example, Key Vault (Microsoft.KeyVault) services will be included in the new plan.</span></span>
3. <span data-ttu-id="98617-120">In the administrator portal, click **Offers** and then select the offer to be updated with an add-on plan.</span><span class="sxs-lookup"><span data-stu-id="98617-120">In the administrator portal, click **Offers** and then select the offer to be updated with an add-on plan.</span></span>

   ![](media/create-add-on-plan/1.PNG)

4.  <span data-ttu-id="98617-121">Scroll to the bottom of the offer properties and select **Add-on plans**.</span><span class="sxs-lookup"><span data-stu-id="98617-121">Scroll to the bottom of the offer properties and select **Add-on plans**.</span></span> <span data-ttu-id="98617-122">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="98617-122">Click **Add**.</span></span>
   
    ![](media/create-add-on-plan/2.PNG)

5. <span data-ttu-id="98617-123">Select the plan to add.</span><span class="sxs-lookup"><span data-stu-id="98617-123">Select the plan to add.</span></span> <span data-ttu-id="98617-124">In this example, the plan is called **Key vault plan**.</span><span class="sxs-lookup"><span data-stu-id="98617-124">In this example, the plan is called **Key vault plan**.</span></span> <span data-ttu-id="98617-125">After selecting the plan, click **Select** to add the plan to the offer.</span><span class="sxs-lookup"><span data-stu-id="98617-125">After selecting the plan, click **Select** to add the plan to the offer.</span></span> <span data-ttu-id="98617-126">You should receive a notification that the plan was added to the offer successfully.</span><span class="sxs-lookup"><span data-stu-id="98617-126">You should receive a notification that the plan was added to the offer successfully.</span></span>
   
    ![](media/create-add-on-plan/3.PNG)

6. <span data-ttu-id="98617-127">Review the list of add-on plans included with the offer to verify that the new add-on plan listed.</span><span class="sxs-lookup"><span data-stu-id="98617-127">Review the list of add-on plans included with the offer to verify that the new add-on plan listed.</span></span>
   
    ![](media/create-add-on-plan/4.PNG)

## <a name="next-steps"></a><span data-ttu-id="98617-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="98617-128">Next steps</span></span>
[<span data-ttu-id="98617-129">Create an offer</span><span class="sxs-lookup"><span data-stu-id="98617-129">Create an offer</span></span>](azure-stack-create-offer.md)