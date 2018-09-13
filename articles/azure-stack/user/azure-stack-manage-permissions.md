---
title: Manage permissions to resources per user in Azure Stack | Microsoft Docs
description: As a service administrator or tenant, learn how to manage RBAC permissions.
services: azure-stack
documentationcenter: ''
author: PatAltimore
manager: femila
editor: ''
ms.assetid: cccac19a-e1bf-4e36-8ac8-2228e8487646
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: patricka
ms.reviewer: ''
ms.openlocfilehash: 2e36f52568d349aeecd47f90bf9431f096cc4fdc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868951"
---
# <a name="manage-access-to-resources-with-azure-stack-role-based-access-control"></a><span data-ttu-id="f5e42-103">Manage access to resources with Azure Stack Role-Based Access Control</span><span class="sxs-lookup"><span data-stu-id="f5e42-103">Manage access to resources with Azure Stack Role-Based Access Control</span></span>

<span data-ttu-id="f5e42-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="f5e42-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="f5e42-105">Azure Stack supports role-based access control (RBAC), the same [security model for access management](https://docs.microsoft.com/azure/role-based-access-control/overview) that Microsoft Azure uses.</span><span class="sxs-lookup"><span data-stu-id="f5e42-105">Azure Stack supports role-based access control (RBAC), the same [security model for access management](https://docs.microsoft.com/azure/role-based-access-control/overview) that Microsoft Azure uses.</span></span> <span data-ttu-id="f5e42-106">You can use RBAC to manage user, group, or application access to subscriptions, resources, and services.</span><span class="sxs-lookup"><span data-stu-id="f5e42-106">You can use RBAC to manage user, group, or application access to subscriptions, resources, and services.</span></span>

## <a name="basics-of-access-management"></a><span data-ttu-id="f5e42-107">Basics of access management</span><span class="sxs-lookup"><span data-stu-id="f5e42-107">Basics of access management</span></span>

<span data-ttu-id="f5e42-108">Role-based access control provides fine-grained access control that you can use to secure your environment.</span><span class="sxs-lookup"><span data-stu-id="f5e42-108">Role-based access control provides fine-grained access control that you can use to secure your environment.</span></span> <span data-ttu-id="f5e42-109">You give users the exact permissions they need by assigning a RBAC role at a certain scope.</span><span class="sxs-lookup"><span data-stu-id="f5e42-109">You give users the exact permissions they need by assigning a RBAC role at a certain scope.</span></span> <span data-ttu-id="f5e42-110">The scope of the role assignment can be a subscription, a resource group, or a single resource.</span><span class="sxs-lookup"><span data-stu-id="f5e42-110">The scope of the role assignment can be a subscription, a resource group, or a single resource.</span></span> <span data-ttu-id="f5e42-111">Read the [Role-Based Access Control in the Azure portal](https://docs.microsoft.com/azure/role-based-access-control/overview) article to get more detailed information about access management.</span><span class="sxs-lookup"><span data-stu-id="f5e42-111">Read the [Role-Based Access Control in the Azure portal](https://docs.microsoft.com/azure/role-based-access-control/overview) article to get more detailed information about access management.</span></span>

### <a name="built-in-roles"></a><span data-ttu-id="f5e42-112">Built-in roles</span><span class="sxs-lookup"><span data-stu-id="f5e42-112">Built-in roles</span></span>

<span data-ttu-id="f5e42-113">Azure Stack has three basic roles that you can apply to all resource types:</span><span class="sxs-lookup"><span data-stu-id="f5e42-113">Azure Stack has three basic roles that you can apply to all resource types:</span></span>

* <span data-ttu-id="f5e42-114">**Owner** can manage everything, including access to resources.</span><span class="sxs-lookup"><span data-stu-id="f5e42-114">**Owner** can manage everything, including access to resources.</span></span>
* <span data-ttu-id="f5e42-115">**Contributor** can manage everything except access to resources.</span><span class="sxs-lookup"><span data-stu-id="f5e42-115">**Contributor** can manage everything except access to resources.</span></span>
* <span data-ttu-id="f5e42-116">**Reader** can view everything, but can’t make any changes.</span><span class="sxs-lookup"><span data-stu-id="f5e42-116">**Reader** can view everything, but can’t make any changes.</span></span>

### <a name="resource-hierarchy-and-inheritance"></a><span data-ttu-id="f5e42-117">Resource hierarchy and inheritance</span><span class="sxs-lookup"><span data-stu-id="f5e42-117">Resource hierarchy and inheritance</span></span>

<span data-ttu-id="f5e42-118">Azure Stack has the following resource hierarchy:</span><span class="sxs-lookup"><span data-stu-id="f5e42-118">Azure Stack has the following resource hierarchy:</span></span>

* <span data-ttu-id="f5e42-119">Each subscription belongs to one directory.</span><span class="sxs-lookup"><span data-stu-id="f5e42-119">Each subscription belongs to one directory.</span></span>
* <span data-ttu-id="f5e42-120">Each resource group belongs to one subscription.</span><span class="sxs-lookup"><span data-stu-id="f5e42-120">Each resource group belongs to one subscription.</span></span>
* <span data-ttu-id="f5e42-121">Each resource belongs to one resource group.</span><span class="sxs-lookup"><span data-stu-id="f5e42-121">Each resource belongs to one resource group.</span></span>

<span data-ttu-id="f5e42-122">Access that you grant at a parent scope is inherited at child scopes.</span><span class="sxs-lookup"><span data-stu-id="f5e42-122">Access that you grant at a parent scope is inherited at child scopes.</span></span> <span data-ttu-id="f5e42-123">For example:</span><span class="sxs-lookup"><span data-stu-id="f5e42-123">For example:</span></span>

* <span data-ttu-id="f5e42-124">You assign the Reader role to an Azure AD group at the subscription scope.</span><span class="sxs-lookup"><span data-stu-id="f5e42-124">You assign the Reader role to an Azure AD group at the subscription scope.</span></span> <span data-ttu-id="f5e42-125">The members of that group can view every resource group and resource in the subscription.</span><span class="sxs-lookup"><span data-stu-id="f5e42-125">The members of that group can view every resource group and resource in the subscription.</span></span>
* <span data-ttu-id="f5e42-126">You assign the Contributor role to an application at the resource group scope.</span><span class="sxs-lookup"><span data-stu-id="f5e42-126">You assign the Contributor role to an application at the resource group scope.</span></span> <span data-ttu-id="f5e42-127">The application can manage resources of all types in that resource group, but not other resource groups in the subscription.</span><span class="sxs-lookup"><span data-stu-id="f5e42-127">The application can manage resources of all types in that resource group, but not other resource groups in the subscription.</span></span>

### <a name="assigning-roles"></a><span data-ttu-id="f5e42-128">Assigning roles</span><span class="sxs-lookup"><span data-stu-id="f5e42-128">Assigning roles</span></span>

<span data-ttu-id="f5e42-129">You can assign more than one role to a user and each role can be associated with a different scope.</span><span class="sxs-lookup"><span data-stu-id="f5e42-129">You can assign more than one role to a user and each role can be associated with a different scope.</span></span> <span data-ttu-id="f5e42-130">For example:</span><span class="sxs-lookup"><span data-stu-id="f5e42-130">For example:</span></span>

* <span data-ttu-id="f5e42-131">You assign TestUser-A the Reader role to Subscription-1.</span><span class="sxs-lookup"><span data-stu-id="f5e42-131">You assign TestUser-A the Reader role to Subscription-1.</span></span>
* <span data-ttu-id="f5e42-132">You assign TestUser-A the Owner role to TestVM-1.</span><span class="sxs-lookup"><span data-stu-id="f5e42-132">You assign TestUser-A the Owner role to TestVM-1.</span></span>

<span data-ttu-id="f5e42-133">The Azure [role assignments](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) article provides detailed information about viewing, assigning, and deleting roles.</span><span class="sxs-lookup"><span data-stu-id="f5e42-133">The Azure [role assignments](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) article provides detailed information about viewing, assigning, and deleting roles.</span></span>

### <a name="resource-hierarchy-and-inheritance"></a><span data-ttu-id="f5e42-134">Resource hierarchy and inheritance</span><span class="sxs-lookup"><span data-stu-id="f5e42-134">Resource hierarchy and inheritance</span></span>

<span data-ttu-id="f5e42-135">Azure Stack has the following resource hierarchy:</span><span class="sxs-lookup"><span data-stu-id="f5e42-135">Azure Stack has the following resource hierarchy:</span></span>

* <span data-ttu-id="f5e42-136">Each subscription belongs to one directory.</span><span class="sxs-lookup"><span data-stu-id="f5e42-136">Each subscription belongs to one directory.</span></span>
* <span data-ttu-id="f5e42-137">Each resource group belongs to one subscription.</span><span class="sxs-lookup"><span data-stu-id="f5e42-137">Each resource group belongs to one subscription.</span></span>
* <span data-ttu-id="f5e42-138">Each resource belongs to one resource group.</span><span class="sxs-lookup"><span data-stu-id="f5e42-138">Each resource belongs to one resource group.</span></span>

<span data-ttu-id="f5e42-139">Access that you grant at a parent scope is inherited at child scopes.</span><span class="sxs-lookup"><span data-stu-id="f5e42-139">Access that you grant at a parent scope is inherited at child scopes.</span></span> <span data-ttu-id="f5e42-140">For example:</span><span class="sxs-lookup"><span data-stu-id="f5e42-140">For example:</span></span>

* <span data-ttu-id="f5e42-141">You assign the **Reader** role to an Azure AD group at the subscription scope.</span><span class="sxs-lookup"><span data-stu-id="f5e42-141">You assign the **Reader** role to an Azure AD group at the subscription scope.</span></span> <span data-ttu-id="f5e42-142">The members of that group can view every resource group and resource in the subscription.</span><span class="sxs-lookup"><span data-stu-id="f5e42-142">The members of that group can view every resource group and resource in the subscription.</span></span>
* <span data-ttu-id="f5e42-143">You assign the **Contributor** role to an application at the resource group scope.</span><span class="sxs-lookup"><span data-stu-id="f5e42-143">You assign the **Contributor** role to an application at the resource group scope.</span></span> <span data-ttu-id="f5e42-144">The application can manage resources of all types in that resource group, but not other resource groups in the subscription.</span><span class="sxs-lookup"><span data-stu-id="f5e42-144">The application can manage resources of all types in that resource group, but not other resource groups in the subscription.</span></span>

### <a name="assigning-roles"></a><span data-ttu-id="f5e42-145">Assigning roles</span><span class="sxs-lookup"><span data-stu-id="f5e42-145">Assigning roles</span></span>

<span data-ttu-id="f5e42-146">You can assign more than one role to a user and each role can be associated with a different scope.</span><span class="sxs-lookup"><span data-stu-id="f5e42-146">You can assign more than one role to a user and each role can be associated with a different scope.</span></span> <span data-ttu-id="f5e42-147">For example:</span><span class="sxs-lookup"><span data-stu-id="f5e42-147">For example:</span></span>

* <span data-ttu-id="f5e42-148">You assign TestUser-A the Reader role to Subscription-1.</span><span class="sxs-lookup"><span data-stu-id="f5e42-148">You assign TestUser-A the Reader role to Subscription-1.</span></span>
* <span data-ttu-id="f5e42-149">You assign TestUser-A the Owner role to TestVM-1.</span><span class="sxs-lookup"><span data-stu-id="f5e42-149">You assign TestUser-A the Owner role to TestVM-1.</span></span>

<span data-ttu-id="f5e42-150">The Azure [role assignments](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) article provides detailed information about viewing, assigning, and deleting roles.</span><span class="sxs-lookup"><span data-stu-id="f5e42-150">The Azure [role assignments](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal) article provides detailed information about viewing, assigning, and deleting roles.</span></span>

## <a name="set-access-permissions-for-a-user"></a><span data-ttu-id="f5e42-151">Set access permissions for a user</span><span class="sxs-lookup"><span data-stu-id="f5e42-151">Set access permissions for a user</span></span>

<span data-ttu-id="f5e42-152">The following steps describe how to configure permissions for a user.</span><span class="sxs-lookup"><span data-stu-id="f5e42-152">The following steps describe how to configure permissions for a user.</span></span>

1. <span data-ttu-id="f5e42-153">Sign in with an account that has owner permissions to the resource you want to manage.</span><span class="sxs-lookup"><span data-stu-id="f5e42-153">Sign in with an account that has owner permissions to the resource you want to manage.</span></span>
2. <span data-ttu-id="f5e42-154">In the left navigation pane, choose **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="f5e42-154">In the left navigation pane, choose **Resource groups**.</span></span>
3. <span data-ttu-id="f5e42-155">Choose the name of the resource group that you want to set permissions on.</span><span class="sxs-lookup"><span data-stu-id="f5e42-155">Choose the name of the resource group that you want to set permissions on.</span></span>
4. <span data-ttu-id="f5e42-156">In the resource group navigation pane, choose **Access control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="f5e42-156">In the resource group navigation pane, choose **Access control (IAM)**.</span></span> <span data-ttu-id="f5e42-157">The **Access control** view lists the Items that have access to the resource group.</span><span class="sxs-lookup"><span data-stu-id="f5e42-157">The **Access control** view lists the Items that have access to the resource group.</span></span> <span data-ttu-id="f5e42-158">You can filter these results, and use a menu bar to Add or Remove permissions.</span><span class="sxs-lookup"><span data-stu-id="f5e42-158">You can filter these results, and use a menu bar to Add or Remove permissions.</span></span>
5. <span data-ttu-id="f5e42-159">On the **Access control** menu bar, choose **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="f5e42-159">On the **Access control** menu bar, choose **+ Add**.</span></span>
6. <span data-ttu-id="f5e42-160">On **Add permissions**:</span><span class="sxs-lookup"><span data-stu-id="f5e42-160">On **Add permissions**:</span></span>

   * <span data-ttu-id="f5e42-161">Choose the role you want to assign from the **Role** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="f5e42-161">Choose the role you want to assign from the **Role** drop-down list.</span></span>
   * <span data-ttu-id="f5e42-162">Choose the resource you want to assign from the **Assign access to** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="f5e42-162">Choose the resource you want to assign from the **Assign access to** drop-down list.</span></span>
   * <span data-ttu-id="f5e42-163">Select the user, group, or application in your directory that you wish to grant access to.</span><span class="sxs-lookup"><span data-stu-id="f5e42-163">Select the user, group, or application in your directory that you wish to grant access to.</span></span> <span data-ttu-id="f5e42-164">You can search the directory with display names, email addresses, and object identifiers.</span><span class="sxs-lookup"><span data-stu-id="f5e42-164">You can search the directory with display names, email addresses, and object identifiers.</span></span>

7. <span data-ttu-id="f5e42-165">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f5e42-165">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5e42-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5e42-166">Next steps</span></span>

[<span data-ttu-id="f5e42-167">Create service principals</span><span class="sxs-lookup"><span data-stu-id="f5e42-167">Create service principals</span></span>](azure-stack-create-service-principals.md)