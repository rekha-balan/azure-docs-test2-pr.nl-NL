---
title: How to give access to Privileged Identity Management - Azure | Microsoft Docs
description: Learn how to add roles to users with the Azure Active Directory Privileged Identity Management extension so they can manage PIM.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: 868cbd1ea40fa48fe11b7d23c8da509e2db09d38
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554260"
---
# <a name="giving-access-to-manage-azure-ad-privileged-identity-management"></a><span data-ttu-id="74133-103">Giving access to manage Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="74133-103">Giving access to manage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="74133-104">The global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span><span class="sxs-lookup"><span data-stu-id="74133-104">The global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span></span> <span data-ttu-id="74133-105">No one else gets write access by default, though, including other global administrators.</span><span class="sxs-lookup"><span data-stu-id="74133-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="74133-106">Other global adminstrators, security administrators, and security readers have read-only access to Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="74133-106">Other global adminstrators, security administrators, and security readers have read-only access to Azure AD PIM.</span></span> <span data-ttu-id="74133-107">To give access to PIM, the first user can assign others to the **Privileged role administrator** role.</span><span class="sxs-lookup"><span data-stu-id="74133-107">To give access to PIM, the first user can assign others to the **Privileged role administrator** role.</span></span> <span data-ttu-id="74133-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span><span class="sxs-lookup"><span data-stu-id="74133-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="74133-109">Managing Azure AD PIM requires Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="74133-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="74133-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="74133-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="74133-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span><span class="sxs-lookup"><span data-stu-id="74133-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-to-manage-pim"></a><span data-ttu-id="74133-112">Give another user access to manage PIM</span><span class="sxs-lookup"><span data-stu-id="74133-112">Give another user access to manage PIM</span></span>
1. <span data-ttu-id="74133-113">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** app on the dashboard.</span><span class="sxs-lookup"><span data-stu-id="74133-113">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** app on the dashboard.</span></span>
2. <span data-ttu-id="74133-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="74133-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Add privileged role administrators - screenshot][1]
3. <span data-ttu-id="74133-116">On the Add managed users blade, step 1 is already complete.</span><span class="sxs-lookup"><span data-stu-id="74133-116">On the Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="74133-117">Select step 2, **Select users** and search for the user you want to add.</span><span class="sxs-lookup"><span data-stu-id="74133-117">Select step 2, **Select users** and search for the user you want to add.</span></span>
   
    ![Select users - screenshot][2]
4. <span data-ttu-id="74133-119">Select the user from the search results, and click **Done**.</span><span class="sxs-lookup"><span data-stu-id="74133-119">Select the user from the search results, and click **Done**.</span></span>
5. <span data-ttu-id="74133-120">Click **OK** to save your selection.</span><span class="sxs-lookup"><span data-stu-id="74133-120">Click **OK** to save your selection.</span></span> <span data-ttu-id="74133-121">The user you have selected will appear in the list of Privileged role administrators.</span><span class="sxs-lookup"><span data-stu-id="74133-121">The user you have selected will appear in the list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="74133-122">Whenever you assign a new role to someone, they are automatically set up as eligible to activate the role.</span><span class="sxs-lookup"><span data-stu-id="74133-122">Whenever you assign a new role to someone, they are automatically set up as eligible to activate the role.</span></span> <span data-ttu-id="74133-123">If you want to make them permanent in the role, click the user in the list.</span><span class="sxs-lookup"><span data-stu-id="74133-123">If you want to make them permanent in the role, click the user in the list.</span></span> <span data-ttu-id="74133-124">Select **make perm** in the user information menu.</span><span class="sxs-lookup"><span data-stu-id="74133-124">Select **make perm** in the user information menu.</span></span>
6. <span data-ttu-id="74133-125">Send the user a link to [Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="74133-125">Send the user a link to [Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="74133-126">Remove another user's access rights for managing PIM</span><span class="sxs-lookup"><span data-stu-id="74133-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="74133-127">Before you remove someone from the privileged role administrator role, always make sure there will still be two users assigned to it.</span><span class="sxs-lookup"><span data-stu-id="74133-127">Before you remove someone from the privileged role administrator role, always make sure there will still be two users assigned to it.</span></span>

1. <span data-ttu-id="74133-128">In the PIM dashboard, click on the role **Privileged role administrator**.</span><span class="sxs-lookup"><span data-stu-id="74133-128">In the PIM dashboard, click on the role **Privileged role administrator**.</span></span>  <span data-ttu-id="74133-129">The list of users currently in that role will be displayed.</span><span class="sxs-lookup"><span data-stu-id="74133-129">The list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="74133-130">Click on the user in the user list.</span><span class="sxs-lookup"><span data-stu-id="74133-130">Click on the user in the user list.</span></span>
3. <span data-ttu-id="74133-131">Click on **Remove**.</span><span class="sxs-lookup"><span data-stu-id="74133-131">Click on **Remove**.</span></span>  <span data-ttu-id="74133-132">You are presented with a confirmation message.</span><span class="sxs-lookup"><span data-stu-id="74133-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="74133-133">Click **Yes** to remove the user from the role.</span><span class="sxs-lookup"><span data-stu-id="74133-133">Click **Yes** to remove the user from the role.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="74133-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="74133-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png


