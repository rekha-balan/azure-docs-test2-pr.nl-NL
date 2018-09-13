---
title: View Azure resource access assignments | Microsoft Docs
description: View and manage all the Role-Based Access Control assignments for any user or group in the Azure portal
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 3/21/2017
ms.author: kgremban
ms.openlocfilehash: e971fa8c899e285d64e22b23191f74b286f52f69
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555710"
---
# <a name="view-access-assignments-for-users-and-groups-in-the-azure-portal---public-preview"></a><span data-ttu-id="88f41-103">View access assignments for users and groups in the Azure portal - Public preview</span><span class="sxs-lookup"><span data-stu-id="88f41-103">View access assignments for users and groups in the Azure portal - Public preview</span></span>
> [!div class="op_single_selector"]
> * [Manage access by user or group](role-based-access-control-manage-assignments.md)
> * [Manage access by resource](role-based-access-control-configure.md)

<span data-ttu-id="88f41-106">With Role-Based Access Control (RBAC) in the Azure Active Directory preview, you can manage access to your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="88f41-106">With Role-Based Access Control (RBAC) in the Azure Active Directory preview, you can manage access to your Azure resources.</span></span> [<span data-ttu-id="88f41-107">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="88f41-107">What's in the preview?</span></span>](active-directory-preview-explainer.md)

<span data-ttu-id="88f41-108">Access assigned with RBAC is fine-grained because there are two ways you can restrict the permissions:</span><span class="sxs-lookup"><span data-stu-id="88f41-108">Access assigned with RBAC is fine-grained because there are two ways you can restrict the permissions:</span></span>

* <span data-ttu-id="88f41-109">**Scope:** RBAC role assignments are scoped to a specific subscription, resource group, or resource.</span><span class="sxs-lookup"><span data-stu-id="88f41-109">**Scope:** RBAC role assignments are scoped to a specific subscription, resource group, or resource.</span></span> <span data-ttu-id="88f41-110">A user given access to a single resource cannot access any other resources in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="88f41-110">A user given access to a single resource cannot access any other resources in the same subscription.</span></span>
* <span data-ttu-id="88f41-111">**Role:** Within the scope of the assignment, access is narrowed even further by assigning a role.</span><span class="sxs-lookup"><span data-stu-id="88f41-111">**Role:** Within the scope of the assignment, access is narrowed even further by assigning a role.</span></span> <span data-ttu-id="88f41-112">Roles can be high-level, like owner, or specific, like virtual machine reader.</span><span class="sxs-lookup"><span data-stu-id="88f41-112">Roles can be high-level, like owner, or specific, like virtual machine reader.</span></span>

<span data-ttu-id="88f41-113">Roles can only be assigned from within the subscription, resource group, or resource that is the scope for the assignment.</span><span class="sxs-lookup"><span data-stu-id="88f41-113">Roles can only be assigned from within the subscription, resource group, or resource that is the scope for the assignment.</span></span> <span data-ttu-id="88f41-114">But you can view all the access assignments for a given user or group in a single place.</span><span class="sxs-lookup"><span data-stu-id="88f41-114">But you can view all the access assignments for a given user or group in a single place.</span></span> <span data-ttu-id="88f41-115">You can have up to 2000 role assignments in each subscription.</span><span class="sxs-lookup"><span data-stu-id="88f41-115">You can have up to 2000 role assignments in each subscription.</span></span> 

<span data-ttu-id="88f41-116">Get more information about how to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="88f41-116">Get more information about how to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md).</span></span>

## <a name="view-access-assignments"></a><span data-ttu-id="88f41-117">View access assignments</span><span class="sxs-lookup"><span data-stu-id="88f41-117">View access assignments</span></span>
<span data-ttu-id="88f41-118">To look up the access assignments for a single user or group, start in Azure Active Directory in the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="88f41-118">To look up the access assignments for a single user or group, start in Azure Active Directory in the [Azure portal](http://portal.azure.com).</span></span>

1. <span data-ttu-id="88f41-119">Select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="88f41-119">Select **Azure Active Directory**.</span></span> <span data-ttu-id="88f41-120">If this option is not visible on your navigation list, select **More Services** and then scroll down to find **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="88f41-120">If this option is not visible on your navigation list, select **More Services** and then scroll down to find **Azure Active Directory**.</span></span>
2. <span data-ttu-id="88f41-121">Select **Users and Groups**, and then either **All users** or **All groups**.</span><span class="sxs-lookup"><span data-stu-id="88f41-121">Select **Users and Groups**, and then either **All users** or **All groups**.</span></span> <span data-ttu-id="88f41-122">For this example, we focus on individual users.</span><span class="sxs-lookup"><span data-stu-id="88f41-122">For this example, we focus on individual users.</span></span>
    <span data-ttu-id="88f41-123">![Manage users and groups in Azure Active Directory - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span><span class="sxs-lookup"><span data-stu-id="88f41-123">![Manage users and groups in Azure Active Directory - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-assignments/rbac_users_groups.png)</span></span>
3. <span data-ttu-id="88f41-124">Search for the user by name or username.</span><span class="sxs-lookup"><span data-stu-id="88f41-124">Search for the user by name or username.</span></span>
4. <span data-ttu-id="88f41-125">Select **Azure resources** on the user blade.</span><span class="sxs-lookup"><span data-stu-id="88f41-125">Select **Azure resources** on the user blade.</span></span> <span data-ttu-id="88f41-126">All the access assignments for that user appear.</span><span class="sxs-lookup"><span data-stu-id="88f41-126">All the access assignments for that user appear.</span></span>

### <a name="read-permissions-to-view-assignments"></a><span data-ttu-id="88f41-127">Read permissions to view assignments</span><span class="sxs-lookup"><span data-stu-id="88f41-127">Read permissions to view assignments</span></span>
<span data-ttu-id="88f41-128">This page only shows the access assignments that you have permission to read.</span><span class="sxs-lookup"><span data-stu-id="88f41-128">This page only shows the access assignments that you have permission to read.</span></span> <span data-ttu-id="88f41-129">For example, you have read access to subscription A and go to the Azure resources blade to check a user's assignments.</span><span class="sxs-lookup"><span data-stu-id="88f41-129">For example, you have read access to subscription A and go to the Azure resources blade to check a user's assignments.</span></span> <span data-ttu-id="88f41-130">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span><span class="sxs-lookup"><span data-stu-id="88f41-130">You can see her access assignments for subscription A, but can't see that she also has access assignments on subscription B.</span></span>

## <a name="delete-access-assignments"></a><span data-ttu-id="88f41-131">Delete access assignments</span><span class="sxs-lookup"><span data-stu-id="88f41-131">Delete access assignments</span></span>
<span data-ttu-id="88f41-132">From this blade, you can delete access assignments that were assigned directly to a user or group.</span><span class="sxs-lookup"><span data-stu-id="88f41-132">From this blade, you can delete access assignments that were assigned directly to a user or group.</span></span> <span data-ttu-id="88f41-133">If the access assignment was inherited from a parent group, you need to go to the resource or subscription and manage the assignment there.</span><span class="sxs-lookup"><span data-stu-id="88f41-133">If the access assignment was inherited from a parent group, you need to go to the resource or subscription and manage the assignment there.</span></span>

1. <span data-ttu-id="88f41-134">From the list of all the access assignments for a user or group, select the one you want to delete.</span><span class="sxs-lookup"><span data-stu-id="88f41-134">From the list of all the access assignments for a user or group, select the one you want to delete.</span></span>
2. <span data-ttu-id="88f41-135">Select **Remove** and then **Yes** to confirm.</span><span class="sxs-lookup"><span data-stu-id="88f41-135">Select **Remove** and then **Yes** to confirm.</span></span>
    <span data-ttu-id="88f41-136">![Remove access assignment - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-assignments/delete_assignment.png)</span><span class="sxs-lookup"><span data-stu-id="88f41-136">![Remove access assignment - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-assignments/delete_assignment.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="88f41-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="88f41-137">Next steps</span></span>

* <span data-ttu-id="88f41-138">Get started with Role-Based Access Control to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md)</span><span class="sxs-lookup"><span data-stu-id="88f41-138">Get started with Role-Based Access Control to [Use role assignments to manage access to your Azure subscription resources](role-based-access-control-configure.md)</span></span>
* <span data-ttu-id="88f41-139">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="88f41-139">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>



