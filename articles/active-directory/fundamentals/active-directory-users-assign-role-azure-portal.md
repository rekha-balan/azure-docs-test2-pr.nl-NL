---
title: Assign a user to administrator roles in Azure Active Directory  | Microsoft Docs
description: How to change user administrative information in Azure Active Directory
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: fundamentals
ms.topic: quickstart
ms.date: 06/25/2018
ms.author: lizross
ms.reviewer: jeffsta
ms.openlocfilehash: ec30f1507bfa45c29709a7f4b7dc1e91aa25ca57
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856624"
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory"></a><span data-ttu-id="59cd6-103">Assign a user to administrator roles in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59cd6-103">Assign a user to administrator roles in Azure Active Directory</span></span>
<span data-ttu-id="59cd6-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="59cd6-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="59cd6-105">For information about adding new users in your organization, see [Add new users to Azure Active Directory](../add-users-azure-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="59cd6-105">For information about adding new users in your organization, see [Add new users to Azure Active Directory](../add-users-azure-active-directory.md).</span></span> <span data-ttu-id="59cd6-106">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span><span class="sxs-lookup"><span data-stu-id="59cd6-106">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="59cd6-107">Assign a role to a user</span><span class="sxs-lookup"><span data-stu-id="59cd6-107">Assign a role to a user</span></span>
1. <span data-ttu-id="59cd6-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin or privileged role admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="59cd6-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin or privileged role admin for the directory.</span></span>

2. <span data-ttu-id="59cd6-109">Select **Azure Active Directory**, select **Users**, and then select a specific user from the list.</span><span class="sxs-lookup"><span data-stu-id="59cd6-109">Select **Azure Active Directory**, select **Users**, and then select a specific user from the list.</span></span>

    ![Opening user management](./media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)

3. <span data-ttu-id="59cd6-111">For the selected user, select **Directory role**, select **Add role**, and then pick the appropriate admin roles from the **Directory roles** list, such as **Conditional access administrator**.</span><span class="sxs-lookup"><span data-stu-id="59cd6-111">For the selected user, select **Directory role**, select **Add role**, and then pick the appropriate admin roles from the **Directory roles** list, such as **Conditional access administrator**.</span></span> <span data-ttu-id="59cd6-112">For more information about administrative roles, see [Assigning administrator roles in Azure AD](../users-groups-roles/directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="59cd6-112">For more information about administrative roles, see [Assigning administrator roles in Azure AD](../users-groups-roles/directory-assign-admin-roles.md).</span></span> 

    ![Assigning a user to a role](./media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)

1. <span data-ttu-id="59cd6-114">Press **Select** to save.</span><span class="sxs-lookup"><span data-stu-id="59cd6-114">Press **Select** to save.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59cd6-115">Next steps</span><span class="sxs-lookup"><span data-stu-id="59cd6-115">Next steps</span></span>
* [<span data-ttu-id="59cd6-116">Quickstart: Add or delete users in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="59cd6-116">Quickstart: Add or delete users in Azure Active Directory</span></span>](add-users-azure-active-directory.md)
* [<span data-ttu-id="59cd6-117">Manage user profiles</span><span class="sxs-lookup"><span data-stu-id="59cd6-117">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="59cd6-118">Add guest users from another directory</span><span class="sxs-lookup"><span data-stu-id="59cd6-118">Add guest users from another directory</span></span>](../b2b/what-is-b2b.md) 
* [<span data-ttu-id="59cd6-119">Assign a user to a role in your Azure AD</span><span class="sxs-lookup"><span data-stu-id="59cd6-119">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)
* [<span data-ttu-id="59cd6-120">Restore a deleted user</span><span class="sxs-lookup"><span data-stu-id="59cd6-120">Restore a deleted user</span></span>](active-directory-users-restore.md)
