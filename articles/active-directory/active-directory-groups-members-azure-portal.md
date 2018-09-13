---
title: Manage the members for a group in Azure Active Directory preview | Microsoft Docs
description: How to add or remove users and devices from a group in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c488d6c77f100b1f782d61e3fb9bbf04ed418ecb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554488"
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a><span data-ttu-id="7e51e-103">Manage group membership for users in your Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="7e51e-103">Manage group membership for users in your Azure Active Directory tenant</span></span>
<span data-ttu-id="7e51e-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD) preview.</span><span class="sxs-lookup"><span data-stu-id="7e51e-104">This article explains how to manage the members for a group in Azure Active Directory (Azure AD) preview.</span></span> [<span data-ttu-id="7e51e-105">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="7e51e-105">What's in the preview?</span></span>](active-directory-preview-explainer.md)

## <a name="how-do-i-find-the-members-and-manage-them"></a><span data-ttu-id="7e51e-106">How do I find the members and manage them?</span><span class="sxs-lookup"><span data-stu-id="7e51e-106">How do I find the members and manage them?</span></span>
1. <span data-ttu-id="7e51e-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="7e51e-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="7e51e-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="7e51e-108">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Opening user management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-members-azure-portal/search-user-management.png)
3. <span data-ttu-id="7e51e-110">On the **Users and groups** blade, select **All groups**.</span><span class="sxs-lookup"><span data-stu-id="7e51e-110">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Opening the groups blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="7e51e-112">On the **Users and groups - All groups** blade, select a group.</span><span class="sxs-lookup"><span data-stu-id="7e51e-112">On the **Users and groups - All groups** blade, select a group.</span></span>
5. <span data-ttu-id="7e51e-113">On the **Group - *groupname*** blade, select **Members**.</span><span class="sxs-lookup"><span data-stu-id="7e51e-113">On the **Group - *groupname*** blade, select **Members**.</span></span>

   ![Opening the Members blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-members-azure-portal/view-group-members.png)
6. <span data-ttu-id="7e51e-115">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span><span class="sxs-lookup"><span data-stu-id="7e51e-115">To add members to the group, on the **Group - Members** blade, select **Add Members**.</span></span>

   ![Add Members command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. <span data-ttu-id="7e51e-117">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span><span class="sxs-lookup"><span data-stu-id="7e51e-117">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="7e51e-118">The **User** box filters the display based on matching your entry to any part of a user or device name.</span><span class="sxs-lookup"><span data-stu-id="7e51e-118">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="7e51e-119">No wildcard characters are accepted in that box.</span><span class="sxs-lookup"><span data-stu-id="7e51e-119">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="7e51e-120">To remove members from the group, on the **Group - Members** blade, select a member.</span><span class="sxs-lookup"><span data-stu-id="7e51e-120">To remove members from the group, on the **Group - Members** blade, select a member.</span></span>
9. <span data-ttu-id="7e51e-121">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span><span class="sxs-lookup"><span data-stu-id="7e51e-121">On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.</span></span>

   ![remove Members command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. <span data-ttu-id="7e51e-123">When you finish changing members for the group, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="7e51e-123">When you finish changing members for the group, select **Save**.</span></span>

## <a name="additional-information"></a><span data-ttu-id="7e51e-124">Additional information</span><span class="sxs-lookup"><span data-stu-id="7e51e-124">Additional information</span></span>
<span data-ttu-id="7e51e-125">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7e51e-125">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="7e51e-126">See existing groups</span><span class="sxs-lookup"><span data-stu-id="7e51e-126">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="7e51e-127">Create a new group and adding members</span><span class="sxs-lookup"><span data-stu-id="7e51e-127">Create a new group and adding members</span></span>](active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="7e51e-128">Manage settings of a group</span><span class="sxs-lookup"><span data-stu-id="7e51e-128">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="7e51e-129">Manage memberships of a group</span><span class="sxs-lookup"><span data-stu-id="7e51e-129">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="7e51e-130">Manage dynamic rules for users in a group</span><span class="sxs-lookup"><span data-stu-id="7e51e-130">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)





