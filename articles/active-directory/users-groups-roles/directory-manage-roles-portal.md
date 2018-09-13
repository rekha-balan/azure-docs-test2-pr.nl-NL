---
title: View members of an administrator role and role permissions in Azure Active Directory | Microsoft Docs
description: You can now see and manage members of an Azure AD administrator role in the portal. For those who frequently manage role assignments.
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 07/10/2018
ms.author: curtand
ms.reviewer: vincesm
ms.custom: it-pro
ms.openlocfilehash: 5a42f48e85eea95211b36e0c08dcb0edb4928a20
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866409"
---
# <a name="view-members-and-descriptions-of-administrator-roles-in-azure-active-directory"></a><span data-ttu-id="60add-104">View members and descriptions of administrator roles in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60add-104">View members and descriptions of administrator roles in Azure Active Directory</span></span>

<span data-ttu-id="60add-105">You can now see and manage all the members of the administrator roles in the Azure Active Directory portal.</span><span class="sxs-lookup"><span data-stu-id="60add-105">You can now see and manage all the members of the administrator roles in the Azure Active Directory portal.</span></span> <span data-ttu-id="60add-106">If you frequently manage role assignments, you will probably prefer this experience.</span><span class="sxs-lookup"><span data-stu-id="60add-106">If you frequently manage role assignments, you will probably prefer this experience.</span></span> <span data-ttu-id="60add-107">And if you ever wondered “What the heck do these roles really do?”, you can see a detailed list of permissions for each of the Azure AD administrator roles.</span><span class="sxs-lookup"><span data-stu-id="60add-107">And if you ever wondered “What the heck do these roles really do?”, you can see a detailed list of permissions for each of the Azure AD administrator roles.</span></span>

<span data-ttu-id="60add-108">It's easy to see your own permissions as well.</span><span class="sxs-lookup"><span data-stu-id="60add-108">It's easy to see your own permissions as well.</span></span> <span data-ttu-id="60add-109">Click **Your role** get quick access to your user page for a list of all your active assigned roles.</span><span class="sxs-lookup"><span data-stu-id="60add-109">Click **Your role** get quick access to your user page for a list of all your active assigned roles.</span></span> <span data-ttu-id="60add-110">Click the ellipsis on the right of each row to open the detailed description of the role.</span><span class="sxs-lookup"><span data-stu-id="60add-110">Click the ellipsis on the right of each row to open the detailed description of the role.</span></span>

![list of roles in Azure AD portal](./media/directory-manage-roles-portal/role-list.png)

<span data-ttu-id="60add-112">Select the entire row to view the list of assigned members.</span><span class="sxs-lookup"><span data-stu-id="60add-112">Select the entire row to view the list of assigned members.</span></span> <span data-ttu-id="60add-113">You can select **Manage in PIM** for additional management capabilities.</span><span class="sxs-lookup"><span data-stu-id="60add-113">You can select **Manage in PIM** for additional management capabilities.</span></span> <span data-ttu-id="60add-114">Privileged Role Administrators can change “Permanent” (always active in the role) assignments to “Eligible” (in the role only when elevated).</span><span class="sxs-lookup"><span data-stu-id="60add-114">Privileged Role Administrators can change “Permanent” (always active in the role) assignments to “Eligible” (in the role only when elevated).</span></span> <span data-ttu-id="60add-115">If you don't have PIM, you can still select **Manage in PIM** to sign up for a trial.</span><span class="sxs-lookup"><span data-stu-id="60add-115">If you don't have PIM, you can still select **Manage in PIM** to sign up for a trial.</span></span> <span data-ttu-id="60add-116">Privileged Identity Management requires an [Azure AD Premium P2 license plan](../privileged-identity-management/subscription-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="60add-116">Privileged Identity Management requires an [Azure AD Premium P2 license plan](../privileged-identity-management/subscription-requirements.md).</span></span>

![list of members of an admin role](./media/directory-manage-roles-portal/member-list.png)

<span data-ttu-id="60add-118">If you are a Global Administrator or a Privileged Role Administrator, you can easily add or remove members, filter the list, or select a member to go to the user page to see their active assigned roles.</span><span class="sxs-lookup"><span data-stu-id="60add-118">If you are a Global Administrator or a Privileged Role Administrator, you can easily add or remove members, filter the list, or select a member to go to the user page to see their active assigned roles.</span></span> 

## <a name="detailed-role-permissions-in-the-portal"></a><span data-ttu-id="60add-119">Detailed role permissions in the portal</span><span class="sxs-lookup"><span data-stu-id="60add-119">Detailed role permissions in the portal</span></span>

<span data-ttu-id="60add-120">When you're viewing a role's members, select **Description** to see the complete list of permissions granted by the role assignment.</span><span class="sxs-lookup"><span data-stu-id="60add-120">When you're viewing a role's members, select **Description** to see the complete list of permissions granted by the role assignment.</span></span> <span data-ttu-id="60add-121">The page includes links to relevant documentation to help guide you through managing directory roles.</span><span class="sxs-lookup"><span data-stu-id="60add-121">The page includes links to relevant documentation to help guide you through managing directory roles.</span></span>

![list of permissions for an admin role](./media/directory-manage-roles-portal/role-description.png)


## <a name="next-steps"></a><span data-ttu-id="60add-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="60add-123">Next steps</span></span>

* <span data-ttu-id="60add-124">Feel free to share with us on the [Azure AD administrative roles forum](https://feedback.azure.com/forums/169401-azure-active-directory?category_id=166032).</span><span class="sxs-lookup"><span data-stu-id="60add-124">Feel free to share with us on the [Azure AD administrative roles forum](https://feedback.azure.com/forums/169401-azure-active-directory?category_id=166032).</span></span>
* <span data-ttu-id="60add-125">For more about roles and Administrator role assignment, see [Assign administrator roles](directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="60add-125">For more about roles and Administrator role assignment, see [Assign administrator roles](directory-assign-admin-roles.md).</span></span>
* <span data-ttu-id="60add-126">For default user permissions, see a [comparison of default guest and member user permissions](../fundamentals/users-default-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="60add-126">For default user permissions, see a [comparison of default guest and member user permissions](../fundamentals/users-default-permissions.md).</span></span>
