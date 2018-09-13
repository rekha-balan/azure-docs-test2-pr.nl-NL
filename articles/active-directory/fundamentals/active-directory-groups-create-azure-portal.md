---
title: Create a group for users in Azure AD | Microsoft Docs
description: How to create a group in Azure Active Directory and add members to the group
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: fundamentals
ms.topic: quickstart
ms.date: 08/04/2017
ms.author: lizross
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 3c71c9c49413045e3a730c10e90ea3c12648b4cb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866405"
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="4ea46-103">Create a group and add members in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4ea46-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-groups-create-azure-portal.md)
> * [PowerShell](../users-groups-roles/groups-settings-v2-cmdlets.md)

<span data-ttu-id="4ea46-106">This article explains how to create and populate a new group in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4ea46-106">This article explains how to create and populate a new group in Azure Active Directory.</span></span> <span data-ttu-id="4ea46-107">Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.</span><span class="sxs-lookup"><span data-stu-id="4ea46-107">Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="4ea46-108">How do I create a group?</span><span class="sxs-lookup"><span data-stu-id="4ea46-108">How do I create a group?</span></span>
1. <span data-ttu-id="4ea46-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="4ea46-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="4ea46-110">Select **All services**, enter **User and groups** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="4ea46-110">Select **All services**, enter **User and groups** in the text box, and then select **Enter**.</span></span>

   ![Opening user management](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="4ea46-112">On the **Users and groups** blade, select **All groups**.</span><span class="sxs-lookup"><span data-stu-id="4ea46-112">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Opening the groups blade](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="4ea46-114">On the **Users and groups - All groups** blade, select the **Add** command.</span><span class="sxs-lookup"><span data-stu-id="4ea46-114">On the **Users and groups - All groups** blade, select the **Add** command.</span></span>

   ![Selecting the Add command](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="4ea46-116">On the **Group** blade, add a name and description for the group.</span><span class="sxs-lookup"><span data-stu-id="4ea46-116">On the **Group** blade, add a name and description for the group.</span></span>
6. <span data-ttu-id="4ea46-117">To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**.</span><span class="sxs-lookup"><span data-stu-id="4ea46-117">To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="4ea46-118">For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](../users-groups-roles/groups-dynamic-membership.md).</span><span class="sxs-lookup"><span data-stu-id="4ea46-118">For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](../users-groups-roles/groups-dynamic-membership.md).</span></span>

   ![Selecting members to add](./media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="4ea46-120">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span><span class="sxs-lookup"><span data-stu-id="4ea46-120">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="4ea46-121">The **User** box filters the display based on matching your entry to any part of a user or device name.</span><span class="sxs-lookup"><span data-stu-id="4ea46-121">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="4ea46-122">No wildcard characters are accepted in that box.</span><span class="sxs-lookup"><span data-stu-id="4ea46-122">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="4ea46-123">When you finish adding members to the group, select **Create** on the **Group** blade.</span><span class="sxs-lookup"><span data-stu-id="4ea46-123">When you finish adding members to the group, select **Create** on the **Group** blade.</span></span>    

   ![Create group confirmation](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a><span data-ttu-id="4ea46-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ea46-125">Next steps</span></span>
<span data-ttu-id="4ea46-126">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4ea46-126">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="4ea46-127">See existing groups</span><span class="sxs-lookup"><span data-stu-id="4ea46-127">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="4ea46-128">Manage settings of a group</span><span class="sxs-lookup"><span data-stu-id="4ea46-128">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="4ea46-129">Manage members of a group</span><span class="sxs-lookup"><span data-stu-id="4ea46-129">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="4ea46-130">Manage memberships of a group</span><span class="sxs-lookup"><span data-stu-id="4ea46-130">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="4ea46-131">Manage dynamic rules for users in a group</span><span class="sxs-lookup"><span data-stu-id="4ea46-131">Manage dynamic rules for users in a group</span></span>](../users-groups-roles/groups-dynamic-membership.md)
