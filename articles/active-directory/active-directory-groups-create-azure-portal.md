---
title: Create a group for users in Azure Active Directory preview | Microsoft Docs
description: How to create a group in Azure Active Directory and add members to the group
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 68e9b362b2db2f3911d4ca60c40d26bfbd80dac1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553748"
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a><span data-ttu-id="44411-103">Create a group and add members in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44411-103">Create a group and add members in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-groups-create-azure-portal.md)
> * [Azure classic portal](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="44411-107">This article explains how to create and populate a new group in the Azure Active Directory (Azure AD) preview.</span><span class="sxs-lookup"><span data-stu-id="44411-107">This article explains how to create and populate a new group in the Azure Active Directory (Azure AD) preview.</span></span> [<span data-ttu-id="44411-108">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="44411-108">What's in the preview?</span></span>](active-directory-preview-explainer.md) <span data-ttu-id="44411-109">Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.</span><span class="sxs-lookup"><span data-stu-id="44411-109">Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="44411-110">How do I create a group?</span><span class="sxs-lookup"><span data-stu-id="44411-110">How do I create a group?</span></span>
1. <span data-ttu-id="44411-111">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="44411-111">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="44411-112">Select **More services**, enter **User and groups** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="44411-112">Select **More services**, enter **User and groups** in the text box, and then select **Enter**.</span></span>

   ![Opening user management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-create-azure-portal/search-user-management.png)
3. <span data-ttu-id="44411-114">On the **Users and groups** blade, select **All groups**.</span><span class="sxs-lookup"><span data-stu-id="44411-114">On the **Users and groups** blade, select **All groups**.</span></span>

   ![Opening the groups blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. <span data-ttu-id="44411-116">On the **Users and groups - All groups** blade, select the **Add** command.</span><span class="sxs-lookup"><span data-stu-id="44411-116">On the **Users and groups - All groups** blade, select the **Add** command.</span></span>

   ![Selecting the Add command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-create-azure-portal/add-group-command.png)
5. <span data-ttu-id="44411-118">On the **Group** blade, add a name and description for the group.</span><span class="sxs-lookup"><span data-stu-id="44411-118">On the **Group** blade, add a name and description for the group.</span></span>
6. <span data-ttu-id="44411-119">To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**.</span><span class="sxs-lookup"><span data-stu-id="44411-119">To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**.</span></span> <span data-ttu-id="44411-120">For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="44411-120">For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).</span></span>

   ![Selecting members to add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-create-azure-portal/select-members.png)
7. <span data-ttu-id="44411-122">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span><span class="sxs-lookup"><span data-stu-id="44411-122">On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group.</span></span> <span data-ttu-id="44411-123">The **User** box filters the display based on matching your entry to any part of a user or device name.</span><span class="sxs-lookup"><span data-stu-id="44411-123">The **User** box filters the display based on matching your entry to any part of a user or device name.</span></span> <span data-ttu-id="44411-124">No wildcard characters are accepted in that box.</span><span class="sxs-lookup"><span data-stu-id="44411-124">No wildcard characters are accepted in that box.</span></span>
8. <span data-ttu-id="44411-125">When you finish adding members to the group, select **Create** on the **Group** blade.</span><span class="sxs-lookup"><span data-stu-id="44411-125">When you finish adding members to the group, select **Create** on the **Group** blade.</span></span>    

   ![Create group confirmation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-create-azure-portal/create-group-confirmation.png)

## <a name="next-steps"></a><span data-ttu-id="44411-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="44411-127">Next steps</span></span>
<span data-ttu-id="44411-128">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="44411-128">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="44411-129">See existing groups</span><span class="sxs-lookup"><span data-stu-id="44411-129">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="44411-130">Manage settings of a group</span><span class="sxs-lookup"><span data-stu-id="44411-130">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="44411-131">Manage members of a group</span><span class="sxs-lookup"><span data-stu-id="44411-131">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="44411-132">Manage memberships of a group</span><span class="sxs-lookup"><span data-stu-id="44411-132">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="44411-133">Manage dynamic rules for users in a group</span><span class="sxs-lookup"><span data-stu-id="44411-133">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)





