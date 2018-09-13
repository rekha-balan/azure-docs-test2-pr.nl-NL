---
title: Assign a user to administrator roles in Azure Active Directory preview | Microsoft Docs
description: Explains how to change user administrative information in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: a1ca1a53-50d8-4bf0-ae8f-73fa1253e2d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 72a701317bb523dcd6355dd12452bbff32105f94
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554414"
---
# <a name="assign-a-user-to-administrator-roles-in-azure-active-directory-preview"></a><span data-ttu-id="30f2f-103">Assign a user to administrator roles in Azure Active Directory preview</span><span class="sxs-lookup"><span data-stu-id="30f2f-103">Assign a user to administrator roles in Azure Active Directory preview</span></span>
<span data-ttu-id="30f2f-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD) preview.</span><span class="sxs-lookup"><span data-stu-id="30f2f-104">This article explains how to assign an administrative role to a user in Azure Active Directory (Azure AD) preview.</span></span> [<span data-ttu-id="30f2f-105">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="30f2f-105">What's in the preview?</span></span>](active-directory-preview-explainer.md) <span data-ttu-id="30f2f-106">For information about adding new users in your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="30f2f-106">For information about adding new users in your organization, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="30f2f-107">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span><span class="sxs-lookup"><span data-stu-id="30f2f-107">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="30f2f-108">Assign a role to a user</span><span class="sxs-lookup"><span data-stu-id="30f2f-108">Assign a role to a user</span></span>
1. <span data-ttu-id="30f2f-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="30f2f-109">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="30f2f-110">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="30f2f-110">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Opening user management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-users-assign-role-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="30f2f-112">On the **Users and groups** blade, select **All users**.</span><span class="sxs-lookup"><span data-stu-id="30f2f-112">On the **Users and groups** blade, select **All users**.</span></span>

   ![Opening the All users blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-users-assign-role-azure-portal/create-users-open-users-blade.png)
4. <span data-ttu-id="30f2f-114">On the **Users and groups - All users** blade, select a user from the list.</span><span class="sxs-lookup"><span data-stu-id="30f2f-114">On the **Users and groups - All users** blade, select a user from the list.</span></span>
5. <span data-ttu-id="30f2f-115">On the blade for the selected user, select **Directory role**, and then assign the user to a role from the **Directory role** list.</span><span class="sxs-lookup"><span data-stu-id="30f2f-115">On the blade for the selected user, select **Directory role**, and then assign the user to a role from the **Directory role** list.</span></span> <span data-ttu-id="30f2f-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="30f2f-116">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>

      ![Assigning a user to a role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-users-assign-role-azure-portal/create-users-assign-role.png)
6. <span data-ttu-id="30f2f-118">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="30f2f-118">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="30f2f-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="30f2f-119">Next steps</span></span>
* [<span data-ttu-id="30f2f-120">Add a user</span><span class="sxs-lookup"><span data-stu-id="30f2f-120">Add a user</span></span>](active-directory-users-create-azure-portal.md)
* [<span data-ttu-id="30f2f-121">Reset a user's password in the new Azure portal</span><span class="sxs-lookup"><span data-stu-id="30f2f-121">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="30f2f-122">Change a user's work information</span><span class="sxs-lookup"><span data-stu-id="30f2f-122">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="30f2f-123">Manage user profiles</span><span class="sxs-lookup"><span data-stu-id="30f2f-123">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="30f2f-124">Delete a user in your Azure AD</span><span class="sxs-lookup"><span data-stu-id="30f2f-124">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)



