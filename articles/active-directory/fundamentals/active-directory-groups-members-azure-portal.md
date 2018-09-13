---
title: Manage the members for a group in Azure AD | Microsoft Docs
description: How to add or remove users and devices from a group in Azure Active Directory
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: fundamentals
ms.topic: quickstart
ms.date: 08/28/2017
ms.author: lizross
ms.custom: it-pro
ms.reviewer: krbain
ms.openlocfilehash: 947b0c11aba211530e3ae25d6617079bcaf2995f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866530"
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="c93a7-103">Manage group membership for users in your Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="c93a7-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="c93a7-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c93a7-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD).</span></span>

## <a name="how-do-i-find-the-members-and-manage-them"></a><span data-ttu-id="c93a7-105">How do I find the members and manage them?</span><span class="sxs-lookup"><span data-stu-id="c93a7-105">How do I find the members and manage them?</span></span>
1. <span data-ttu-id="c93a7-106">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="c93a7-106">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="c93a7-107">Select **All services**, enter **Users and groups** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c93a7-107">Select **All services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Opening user management](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="c93a7-109">On the **Users and groups** blade, select **All groups**.</span><span class="sxs-lookup"><span data-stu-id="c93a7-109">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Opening the groups blade](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="c93a7-111">On the **Users and groups - All groups** blade, select a group.</span><span class="sxs-lookup"><span data-stu-id="c93a7-111">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="c93a7-112">On the **Group - *groupname*** blade, select **Members**.</span><span class="sxs-lookup"><span data-stu-id="c93a7-112">On the **Group - *groupname*** blade, select **Members**.</span></span>

   ![Opening the Members blade](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="c93a7-114">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span><span class="sxs-lookup"><span data-stu-id="c93a7-114">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span></span>

   ![Add Members command](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="c93a7-116">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span><span class="sxs-lookup"><span data-stu-id="c93a7-116">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="c93a7-117">The **User** box filters the display based on matching your entry to any part of a user or device name.</span><span class="sxs-lookup"><span data-stu-id="c93a7-117">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="c93a7-118">No wildcard characters are accepted in that box.</span><span class="sxs-lookup"><span data-stu-id="c93a7-118">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="c93a7-119">To remove members from the group, on the **Group - Members** blade, select a member.</span><span class="sxs-lookup"><span data-stu-id="c93a7-119">To remove members from the group, on the **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="c93a7-120">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span><span class="sxs-lookup"><span data-stu-id="c93a7-120">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![remove Members command](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="c93a7-122">When you finish changing members for the group, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="c93a7-122">When you finish changing members for the group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="c93a7-123">Additional information</span><span class="sxs-lookup"><span data-stu-id="c93a7-123">Additional information</span></span>
<span data-ttu-id="c93a7-124">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c93a7-124">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="c93a7-125">See existing groups</span><span class="sxs-lookup"><span data-stu-id="c93a7-125">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="c93a7-126">Create a new group and adding members</span><span class="sxs-lookup"><span data-stu-id="c93a7-126">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="c93a7-127">Manage settings of a group</span><span class="sxs-lookup"><span data-stu-id="c93a7-127">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="c93a7-128">Manage memberships of a group</span><span class="sxs-lookup"><span data-stu-id="c93a7-128">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="c93a7-129">Manage dynamic rules for users in a group</span><span class="sxs-lookup"><span data-stu-id="c93a7-129">Manage dynamic rules for users in a group</span></span>](../users-groups-roles/groups-dynamic-membership.md)
