---
title: Manage the groups your group belongs to in Azure Active Directory preview | Microsoft Docs
description: Groups can contain other groups in Azure Active Directory. Here's how to manage those memberships.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0bc64ab2a7b9bc43dc48c116b5b3b0a6e0701ef
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554952"
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a><span data-ttu-id="1c5c5-104">Manage to which groups a group belongs in your Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="1c5c5-104">Manage to which groups a group belongs in your Azure Active Directory tenant</span></span>
<span data-ttu-id="1c5c5-105">Groups can contain other groups in Azure Active Directory preview.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-105">Groups can contain other groups in Azure Active Directory preview.</span></span> [<span data-ttu-id="1c5c5-106">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="1c5c5-106">What's in the preview?</span></span>](active-directory-preview-explainer.md) <span data-ttu-id="1c5c5-107">Here's how to manage those memberships.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-107">Here's how to manage those memberships.</span></span>

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a><span data-ttu-id="1c5c5-108">How do I find the groups my group is a member of?</span><span class="sxs-lookup"><span data-stu-id="1c5c5-108">How do I find the groups my group is a member of?</span></span>
1. <span data-ttu-id="1c5c5-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="1c5c5-110">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-110">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Opening user management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. <span data-ttu-id="1c5c5-112">On the **Users and groups** blade, select **All groups**.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-112">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Opening the groups blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="1c5c5-114">On the **Users and groups - All groups** blade, select a group.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-114">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="1c5c5-115">On the **Group - *groupname*** blade, select **Group memberships**.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-115">On the **Group - *groupname*** blade, select **Group memberships**.</span></span>

   ![Opening the group memberships blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. <span data-ttu-id="1c5c5-117">To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-117">To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.</span></span>
7. <span data-ttu-id="1c5c5-118">Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-118">Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade.</span></span> <span data-ttu-id="1c5c5-119">You can add your group to only one group at a time.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-119">You can add your group to only one group at a time.</span></span> <span data-ttu-id="1c5c5-120">The **User** box filters the display based on matching your entry to any part of a user or device name.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-120">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="1c5c5-121">No wildcard characters are accepted in that box.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-121">No wildcard characters are accepted in that box.</span></span>

   ![Add a group membership](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. <span data-ttu-id="1c5c5-123">To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-123">To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.</span></span>
9. <span data-ttu-id="1c5c5-124">On the ***groupname*** blade, select the **Remove** command, and confirm your choice at the prompt.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-124">On the ***groupname*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![remove membership command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. <span data-ttu-id="1c5c5-126">When you finish changing group memberships for your group, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-126">When you finish changing group memberships for your group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="1c5c5-127">Additional information</span><span class="sxs-lookup"><span data-stu-id="1c5c5-127">Additional information</span></span>
<span data-ttu-id="1c5c5-128">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1c5c5-128">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="1c5c5-129">See existing groups</span><span class="sxs-lookup"><span data-stu-id="1c5c5-129">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="1c5c5-130">Create a new group and adding members</span><span class="sxs-lookup"><span data-stu-id="1c5c5-130">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="1c5c5-131">Manage settings of a group</span><span class="sxs-lookup"><span data-stu-id="1c5c5-131">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="1c5c5-132">Manage members of a group</span><span class="sxs-lookup"><span data-stu-id="1c5c5-132">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="1c5c5-133">Manage dynamic rules for users in a group</span><span class="sxs-lookup"><span data-stu-id="1c5c5-133">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)





