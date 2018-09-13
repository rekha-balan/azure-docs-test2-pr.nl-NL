---
title: Eligible assignments and resource visibility in PIM - Azure | Microsoft Docs
description: Describes how to assign members as eligible for Azure resource roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: markwahl-msft
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: pim
ms.date: 04/02/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: fb52bc92c86261831d0e8d8e9e863a4863fe8fb9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856587"
---
# <a name="eligible-assignments-and-resource-visibility-in-pim"></a><span data-ttu-id="46d37-103">Eligible assignments and resource visibility in PIM</span><span class="sxs-lookup"><span data-stu-id="46d37-103">Eligible assignments and resource visibility in PIM</span></span>

<span data-ttu-id="46d37-104">Privileged Identity Management (PIM) for Azure resource roles provides enhanced security for organizations that have critical Azure resources.</span><span class="sxs-lookup"><span data-stu-id="46d37-104">Privileged Identity Management (PIM) for Azure resource roles provides enhanced security for organizations that have critical Azure resources.</span></span> <span data-ttu-id="46d37-105">Resource administrators can use PIM to assign members as eligible for resource roles.</span><span class="sxs-lookup"><span data-stu-id="46d37-105">Resource administrators can use PIM to assign members as eligible for resource roles.</span></span> <span data-ttu-id="46d37-106">Learn more about the different assignment types and assignment states for Azure resource roles in the following sections.</span><span class="sxs-lookup"><span data-stu-id="46d37-106">Learn more about the different assignment types and assignment states for Azure resource roles in the following sections.</span></span> 

## <a name="assignment-types"></a><span data-ttu-id="46d37-107">Assignment types</span><span class="sxs-lookup"><span data-stu-id="46d37-107">Assignment types</span></span>

<span data-ttu-id="46d37-108">PIM for Azure resources provides two distinct assignment types:</span><span class="sxs-lookup"><span data-stu-id="46d37-108">PIM for Azure resources provides two distinct assignment types:</span></span>

- <span data-ttu-id="46d37-109">Eligible</span><span class="sxs-lookup"><span data-stu-id="46d37-109">Eligible</span></span>
- <span data-ttu-id="46d37-110">Active</span><span class="sxs-lookup"><span data-stu-id="46d37-110">Active</span></span>

<span data-ttu-id="46d37-111">Eligible assignments require the member of the role to perform an action to use the role.</span><span class="sxs-lookup"><span data-stu-id="46d37-111">Eligible assignments require the member of the role to perform an action to use the role.</span></span> <span data-ttu-id="46d37-112">Actions might include succeeding a multi-factor authentication check, providing a business justification, or requesting approval from designated approvers.</span><span class="sxs-lookup"><span data-stu-id="46d37-112">Actions might include succeeding a multi-factor authentication check, providing a business justification, or requesting approval from designated approvers.</span></span>

<span data-ttu-id="46d37-113">Active assignments don't require the member to perform any action to use the role.</span><span class="sxs-lookup"><span data-stu-id="46d37-113">Active assignments don't require the member to perform any action to use the role.</span></span> <span data-ttu-id="46d37-114">Members assigned as active have the privileges assigned to the role at all times.</span><span class="sxs-lookup"><span data-stu-id="46d37-114">Members assigned as active have the privileges assigned to the role at all times.</span></span>

## <a name="assignment-duration"></a><span data-ttu-id="46d37-115">Assignment duration</span><span class="sxs-lookup"><span data-stu-id="46d37-115">Assignment duration</span></span>

<span data-ttu-id="46d37-116">Resource administrators can choose from two options for each assignment type when they configure PIM settings for a role.</span><span class="sxs-lookup"><span data-stu-id="46d37-116">Resource administrators can choose from two options for each assignment type when they configure PIM settings for a role.</span></span> <span data-ttu-id="46d37-117">These options become the default maximum duration when a member is assigned to the role in PIM.</span><span class="sxs-lookup"><span data-stu-id="46d37-117">These options become the default maximum duration when a member is assigned to the role in PIM.</span></span> 

<span data-ttu-id="46d37-118">An administrator can choose one of these assignment types:</span><span class="sxs-lookup"><span data-stu-id="46d37-118">An administrator can choose one of these assignment types:</span></span>

- <span data-ttu-id="46d37-119">Allow permanent eligible assignment</span><span class="sxs-lookup"><span data-stu-id="46d37-119">Allow permanent eligible assignment</span></span>
- <span data-ttu-id="46d37-120">Allow permanent active assignment</span><span class="sxs-lookup"><span data-stu-id="46d37-120">Allow permanent active assignment</span></span>

<span data-ttu-id="46d37-121">Or, an administrator can choose one of these assignment types:</span><span class="sxs-lookup"><span data-stu-id="46d37-121">Or, an administrator can choose one of these assignment types:</span></span>

- <span data-ttu-id="46d37-122">Expire eligible assignments after</span><span class="sxs-lookup"><span data-stu-id="46d37-122">Expire eligible assignments after</span></span>
- <span data-ttu-id="46d37-123">Expire active assignments after</span><span class="sxs-lookup"><span data-stu-id="46d37-123">Expire active assignments after</span></span>

<span data-ttu-id="46d37-124">If a resource administrator chooses **Allow permanent eligible assignment** or **Allow permanent active assignment**, all administrators that assign members to the resource can assign permanent memberships.</span><span class="sxs-lookup"><span data-stu-id="46d37-124">If a resource administrator chooses **Allow permanent eligible assignment** or **Allow permanent active assignment**, all administrators that assign members to the resource can assign permanent memberships.</span></span>

<span data-ttu-id="46d37-125">If a resource administrator chooses **Expire eligible assignments after** or **Expire active assignments after**, the resource administrator controls the assignment lifecycle by requiring that all assignments have a specified start and end date.</span><span class="sxs-lookup"><span data-stu-id="46d37-125">If a resource administrator chooses **Expire eligible assignments after** or **Expire active assignments after**, the resource administrator controls the assignment lifecycle by requiring that all assignments have a specified start and end date.</span></span>

> [!NOTE] 
> <span data-ttu-id="46d37-126">All assignments that have a specified end date can be renewed by resource administrators.</span><span class="sxs-lookup"><span data-stu-id="46d37-126">All assignments that have a specified end date can be renewed by resource administrators.</span></span> <span data-ttu-id="46d37-127">Also, members can initiate self-service requests to [extend or renew assignments](pim-resource-roles-renew-extend.md).</span><span class="sxs-lookup"><span data-stu-id="46d37-127">Also, members can initiate self-service requests to [extend or renew assignments](pim-resource-roles-renew-extend.md).</span></span>


## <a name="assignment-states"></a><span data-ttu-id="46d37-128">Assignment states</span><span class="sxs-lookup"><span data-stu-id="46d37-128">Assignment states</span></span>

<span data-ttu-id="46d37-129">PIM for Azure resources has two distinct assignment states that appear on the **Active roles** tab in the **My roles**, **Roles**, and **Members** views of PIM.</span><span class="sxs-lookup"><span data-stu-id="46d37-129">PIM for Azure resources has two distinct assignment states that appear on the **Active roles** tab in the **My roles**, **Roles**, and **Members** views of PIM.</span></span> <span data-ttu-id="46d37-130">These states are:</span><span class="sxs-lookup"><span data-stu-id="46d37-130">These states are:</span></span>

- <span data-ttu-id="46d37-131">Assigned</span><span class="sxs-lookup"><span data-stu-id="46d37-131">Assigned</span></span>
- <span data-ttu-id="46d37-132">Activated</span><span class="sxs-lookup"><span data-stu-id="46d37-132">Activated</span></span>

<span data-ttu-id="46d37-133">When you view a membership that's listed in **Active roles**, you can use the value in the **STATE** column to differentiate between users that are **Assigned** as active and users that **Activated** an eligible assignment, and are now active.</span><span class="sxs-lookup"><span data-stu-id="46d37-133">When you view a membership that's listed in **Active roles**, you can use the value in the **STATE** column to differentiate between users that are **Assigned** as active and users that **Activated** an eligible assignment, and are now active.</span></span>

## <a name="azure-resource-role-approval-workflow"></a><span data-ttu-id="46d37-134">Azure resource role approval workflow</span><span class="sxs-lookup"><span data-stu-id="46d37-134">Azure resource role approval workflow</span></span>

<span data-ttu-id="46d37-135">With the approval workflow in PIM for Azure resource roles, administrators can further protect or restrict access to critical resources.</span><span class="sxs-lookup"><span data-stu-id="46d37-135">With the approval workflow in PIM for Azure resource roles, administrators can further protect or restrict access to critical resources.</span></span> <span data-ttu-id="46d37-136">That is, administrators can require approval to activate role assignments.</span><span class="sxs-lookup"><span data-stu-id="46d37-136">That is, administrators can require approval to activate role assignments.</span></span>

<span data-ttu-id="46d37-137">The concept of a resource hierarchy is unique to Azure resource roles.</span><span class="sxs-lookup"><span data-stu-id="46d37-137">The concept of a resource hierarchy is unique to Azure resource roles.</span></span> <span data-ttu-id="46d37-138">This hierarchy enables the inheritance of role assignments from a parent resource object downward to all child resources within the parent container.</span><span class="sxs-lookup"><span data-stu-id="46d37-138">This hierarchy enables the inheritance of role assignments from a parent resource object downward to all child resources within the parent container.</span></span> 

<span data-ttu-id="46d37-139">For example: Bob, a resource administrator, uses PIM to assign Alice as an eligible member to the owner role in the Contoso subscription.</span><span class="sxs-lookup"><span data-stu-id="46d37-139">For example: Bob, a resource administrator, uses PIM to assign Alice as an eligible member to the owner role in the Contoso subscription.</span></span> <span data-ttu-id="46d37-140">With this assignment, Alice is an eligible owner of all resource group containers within the Contoso subscription.</span><span class="sxs-lookup"><span data-stu-id="46d37-140">With this assignment, Alice is an eligible owner of all resource group containers within the Contoso subscription.</span></span> <span data-ttu-id="46d37-141">Alice is also an eligible owner of all resources (like virtual machines) within each resource group of the subscription.</span><span class="sxs-lookup"><span data-stu-id="46d37-141">Alice is also an eligible owner of all resources (like virtual machines) within each resource group of the subscription.</span></span>

<span data-ttu-id="46d37-142">Let's assume there are three resource groups in the Contoso subscription: Fabrikam Test, Fabrikam Dev, and Fabrikam Prod. Each of these resource groups contains a single virtual machine.</span><span class="sxs-lookup"><span data-stu-id="46d37-142">Let's assume there are three resource groups in the Contoso subscription: Fabrikam Test, Fabrikam Dev, and Fabrikam Prod. Each of these resource groups contains a single virtual machine.</span></span>

<span data-ttu-id="46d37-143">PIM settings are configured for each role of a resource.</span><span class="sxs-lookup"><span data-stu-id="46d37-143">PIM settings are configured for each role of a resource.</span></span> <span data-ttu-id="46d37-144">Unlike assignments, these settings are not inherited, and apply strictly to the  resource role.</span><span class="sxs-lookup"><span data-stu-id="46d37-144">Unlike assignments, these settings are not inherited, and apply strictly to the  resource role.</span></span>

<span data-ttu-id="46d37-145">Continuing with the example: Bob uses PIM to require all members in the owner role of the Contoso subscription request approval to be activated.</span><span class="sxs-lookup"><span data-stu-id="46d37-145">Continuing with the example: Bob uses PIM to require all members in the owner role of the Contoso subscription request approval to be activated.</span></span> <span data-ttu-id="46d37-146">To help protect the resources in the Fabrikam Prod resource group, Bob also requires approval for members of the owner role of this resource.</span><span class="sxs-lookup"><span data-stu-id="46d37-146">To help protect the resources in the Fabrikam Prod resource group, Bob also requires approval for members of the owner role of this resource.</span></span> <span data-ttu-id="46d37-147">The owner roles in Fabrikam Test and Fabrikam Dev do not require approval for activation.</span><span class="sxs-lookup"><span data-stu-id="46d37-147">The owner roles in Fabrikam Test and Fabrikam Dev do not require approval for activation.</span></span>

<span data-ttu-id="46d37-148">When Alice requests activation of her owner role for the Contoso subscription, an approver must approve or deny her request before she becomes active in the role.</span><span class="sxs-lookup"><span data-stu-id="46d37-148">When Alice requests activation of her owner role for the Contoso subscription, an approver must approve or deny her request before she becomes active in the role.</span></span> <span data-ttu-id="46d37-149">If Alice decides to [scope her activation](pim-resource-roles-activate-your-roles.md) to the Fabrikam Prod resource group, an approver must approve or deny this request, too.</span><span class="sxs-lookup"><span data-stu-id="46d37-149">If Alice decides to [scope her activation](pim-resource-roles-activate-your-roles.md) to the Fabrikam Prod resource group, an approver must approve or deny this request, too.</span></span> <span data-ttu-id="46d37-150">But if Alice decides to scope her activation to either or both Fabrikam Test or Fabrikam Dev, approval is not required.</span><span class="sxs-lookup"><span data-stu-id="46d37-150">But if Alice decides to scope her activation to either or both Fabrikam Test or Fabrikam Dev, approval is not required.</span></span>

<span data-ttu-id="46d37-151">The approval workflow might not be necessary for all members of a role.</span><span class="sxs-lookup"><span data-stu-id="46d37-151">The approval workflow might not be necessary for all members of a role.</span></span> <span data-ttu-id="46d37-152">Consider a scenario where your organization hires several contract associates to help with the development of an application that will run in an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="46d37-152">Consider a scenario where your organization hires several contract associates to help with the development of an application that will run in an Azure subscription.</span></span> <span data-ttu-id="46d37-153">As a resource administrator, you want employees to have eligible access without approval required, but the contract associates must request approval.</span><span class="sxs-lookup"><span data-stu-id="46d37-153">As a resource administrator, you want employees to have eligible access without approval required, but the contract associates must request approval.</span></span> <span data-ttu-id="46d37-154">To configure approval workflow for only the contract associates, you can create a custom role with the same permissions as the role assigned to employees.</span><span class="sxs-lookup"><span data-stu-id="46d37-154">To configure approval workflow for only the contract associates, you can create a custom role with the same permissions as the role assigned to employees.</span></span> <span data-ttu-id="46d37-155">You can require approval to activate that custom role.</span><span class="sxs-lookup"><span data-stu-id="46d37-155">You can require approval to activate that custom role.</span></span> <span data-ttu-id="46d37-156">[Learn more about custom roles](pim-resource-roles-custom-role-policy.md).</span><span class="sxs-lookup"><span data-stu-id="46d37-156">[Learn more about custom roles](pim-resource-roles-custom-role-policy.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="46d37-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="46d37-157">Next steps</span></span>

- [<span data-ttu-id="46d37-158">Assign Azure resource roles in PIM</span><span class="sxs-lookup"><span data-stu-id="46d37-158">Assign Azure resource roles in PIM</span></span>](pim-resource-roles-assign-roles.md)
