---
title: Add new users to Azure Active Directory preview| Microsoft Docs
description: Explains how to add new users or change user information in Azure Active Directory.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 7b058869011ef1bfd8683500605b27e1fbf4a554
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669231"
---
# <a name="add-new-users-to-azure-active-directory-preview"></a><span data-ttu-id="86145-103">Add new users to Azure Active Directory preview</span><span class="sxs-lookup"><span data-stu-id="86145-103">Add new users to Azure Active Directory preview</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-users-create-azure-portal.md)
> * [Azure classic portal](active-directory-create-users.md)
>
>

<span data-ttu-id="86145-106">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD) preview.</span><span class="sxs-lookup"><span data-stu-id="86145-106">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD) preview.</span></span> [<span data-ttu-id="86145-107">What's in the preview?</span><span class="sxs-lookup"><span data-stu-id="86145-107">What's in the preview?</span></span>](active-directory-preview-explainer.md)

1. <span data-ttu-id="86145-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="86145-108">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="86145-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span><span class="sxs-lookup"><span data-stu-id="86145-109">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

   ![Opening user management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-users-create-azure-portal/create-users-user-management.png)
3. <span data-ttu-id="86145-111">On the **Users and groups** blade, select **All users**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="86145-111">On the **Users and groups** blade, select **All users**, and then select **Add**.</span></span>

   ![Selecting the Add command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-users-create-azure-portal/create-users-add-command.png)
4. <span data-ttu-id="86145-113">Enter details for the user, such as **Name** and **User name**.</span><span class="sxs-lookup"><span data-stu-id="86145-113">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="86145-114">The domain name portion of the user name must either be the initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span><span class="sxs-lookup"><span data-stu-id="86145-114">The domain name portion of the user name must either be the initial default domain name "foo.onmicrosoft.com" domain name, or a verified, non-federated domain name such as "contoso.com."</span></span>
5. <span data-ttu-id="86145-115">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span><span class="sxs-lookup"><span data-stu-id="86145-115">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="86145-116">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span><span class="sxs-lookup"><span data-stu-id="86145-116">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="86145-117">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="86145-117">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="86145-118">On the **User** blade, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="86145-118">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="86145-119">Securely distribute the generated password to the new user so that the user can sign in.</span><span class="sxs-lookup"><span data-stu-id="86145-119">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

### <a name="next-steps"></a><span data-ttu-id="86145-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="86145-120">Next steps</span></span>
* [<span data-ttu-id="86145-121">Add an external user</span><span class="sxs-lookup"><span data-stu-id="86145-121">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)
* [<span data-ttu-id="86145-122">Reset a user's password in the new Azure portal</span><span class="sxs-lookup"><span data-stu-id="86145-122">Reset a user's password in the new Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
* [<span data-ttu-id="86145-123">Change a user's work information</span><span class="sxs-lookup"><span data-stu-id="86145-123">Change a user's work information</span></span>](active-directory-users-work-info-azure-portal.md)
* [<span data-ttu-id="86145-124">Manage user profiles</span><span class="sxs-lookup"><span data-stu-id="86145-124">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="86145-125">Delete a user in your Azure AD</span><span class="sxs-lookup"><span data-stu-id="86145-125">Delete a user in your Azure AD</span></span>](active-directory-users-delete-user-azure-portal.md)
* [<span data-ttu-id="86145-126">Assign a user to a role in your Azure AD</span><span class="sxs-lookup"><span data-stu-id="86145-126">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)


