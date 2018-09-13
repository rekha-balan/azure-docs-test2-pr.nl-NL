---
title: Manage the groups your group belongs to in Azure AD | Microsoft Docs
description: Groups can contain other groups in Azure Active Directory. Here's how to manage those memberships.
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: fundamentals
ms.topic: quickstart
ms.date: 10/10/2017
ms.author: lizross
ms.custom: it-pro
ms.reviewer: krbain
ms.openlocfilehash: 8a71677ae3ceb5617f0a817a8eff438d5e3f2774
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870883"
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="09ed7-104">Manage to which groups a group belongs in your Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="09ed7-104">Manage to which groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="09ed7-105">Groups can contain other groups in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="09ed7-105">Groups can contain other groups in Azure Active Directory.</span></span> <span data-ttu-id="09ed7-106">Here's how to manage those memberships.</span><span class="sxs-lookup"><span data-stu-id="09ed7-106">Here's how to manage those memberships.</span></span>

## <a name="how-do-i-find-the-groups-of-which-my-group-is-a-member"></a><span data-ttu-id="09ed7-107">How do I find the groups of which my group is a member?</span><span class="sxs-lookup"><span data-stu-id="09ed7-107">How do I find the groups of which my group is a member?</span></span>
1. <span data-ttu-id="09ed7-108">Sign in to the [Azure AD admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="09ed7-108">Sign in to the [Azure AD admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="09ed7-109">Select **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="09ed7-109">Select **Users and groups**.</span></span>

   ![Opening users and groups image](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
1. <span data-ttu-id="09ed7-111">Select **All groups**.</span><span class="sxs-lookup"><span data-stu-id="09ed7-111">Select **All groups**.</span></span>

   ![Selecting groups image](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
1. <span data-ttu-id="09ed7-113">Select a group.</span><span class="sxs-lookup"><span data-stu-id="09ed7-113">Select a group.</span></span>
2. <span data-ttu-id="09ed7-114">Select **Group memberships**.</span><span class="sxs-lookup"><span data-stu-id="09ed7-114">Select **Group memberships**.</span></span>

   ![Opening group memberships image](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
1. <span data-ttu-id="09ed7-116">To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.</span><span class="sxs-lookup"><span data-stu-id="09ed7-116">To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.</span></span>
2. <span data-ttu-id="09ed7-117">Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="09ed7-117">Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade.</span></span> <span data-ttu-id="09ed7-118">You can add your group to only one group at a time.</span><span class="sxs-lookup"><span data-stu-id="09ed7-118">You can add your group to only one group at a time.</span></span> <span data-ttu-id="09ed7-119">The **User** box filters the display based on matching your entry to any part of a user or device name.</span><span class="sxs-lookup"><span data-stu-id="09ed7-119">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="09ed7-120">No wildcard characters are accepted in that box.</span><span class="sxs-lookup"><span data-stu-id="09ed7-120">No wildcard characters are accepted in that box.</span></span>

   ![Add a group membership](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="09ed7-122">To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.</span><span class="sxs-lookup"><span data-stu-id="09ed7-122">To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="09ed7-123">Select the **Remove** command, and confirm your choice at the prompt.</span><span class="sxs-lookup"><span data-stu-id="09ed7-123">Select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![remove membership command](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="09ed7-125">When you finish changing group memberships for your group, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="09ed7-125">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="09ed7-126">Additional information</span><span class="sxs-lookup"><span data-stu-id="09ed7-126">Additional information</span></span>
<span data-ttu-id="09ed7-127">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="09ed7-127">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="09ed7-128">See existing groups</span><span class="sxs-lookup"><span data-stu-id="09ed7-128">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="09ed7-129">Create a new group and adding members</span><span class="sxs-lookup"><span data-stu-id="09ed7-129">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="09ed7-130">Manage settings of a group</span><span class="sxs-lookup"><span data-stu-id="09ed7-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="09ed7-131">Manage members of a group</span><span class="sxs-lookup"><span data-stu-id="09ed7-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="09ed7-132">Manage dynamic rules for users in a group</span><span class="sxs-lookup"><span data-stu-id="09ed7-132">Manage dynamic rules for users in a group</span></span>](../users-groups-roles/groups-dynamic-membership.md)
