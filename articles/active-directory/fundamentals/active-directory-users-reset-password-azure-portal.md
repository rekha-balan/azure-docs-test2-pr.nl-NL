---
title: Password reset in Azure Active Directory | Microsoft Docs
description: Administrator initiated password reset for a user in Azure Active Directory
services: active-directory
documentationcenter: ''
author: MicrosoftGuyJFlo
manager: mtillman
editor: ''
ms.assetid: fad5624b-2f13-4abc-b3d4-b347903a8f16
ms.service: active-directory
ms.component: fundamentals
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2017
ms.author: joflore
ms.reviewer: sahenry
ms.custom: it-pro
ms.openlocfilehash: 689ab264e56bc8559db6237eee19566e9e3c429f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867426"
---
# <a name="reset-the-password-for-a-user-in-azure-active-directory"></a><span data-ttu-id="1aa77-103">Reset the password for a user in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1aa77-103">Reset the password for a user in Azure Active Directory</span></span>

<span data-ttu-id="1aa77-104">Administrators may need to reset a user's password in cases where they forgot, were locked out, or other scenarios.</span><span class="sxs-lookup"><span data-stu-id="1aa77-104">Administrators may need to reset a user's password in cases where they forgot, were locked out, or other scenarios.</span></span> <span data-ttu-id="1aa77-105">The steps that follow guide you through resetting a user's password.</span><span class="sxs-lookup"><span data-stu-id="1aa77-105">The steps that follow guide you through resetting a user's password.</span></span>

## <a name="how-to-reset-the-password-for-a-user"></a><span data-ttu-id="1aa77-106">How to reset the password for a user</span><span class="sxs-lookup"><span data-stu-id="1aa77-106">How to reset the password for a user</span></span>

1. <span data-ttu-id="1aa77-107">Sign in to the [Azure AD Admin Center](https://aad.portal.azure.com) with an account that has directory permissions to reset user passwords.</span><span class="sxs-lookup"><span data-stu-id="1aa77-107">Sign in to the [Azure AD Admin Center](https://aad.portal.azure.com) with an account that has directory permissions to reset user passwords.</span></span>
2. <span data-ttu-id="1aa77-108">Select  **Azure Active Directory** > **Users and groups** > **All users**.</span><span class="sxs-lookup"><span data-stu-id="1aa77-108">Select  **Azure Active Directory** > **Users and groups** > **All users**.</span></span>
3. <span data-ttu-id="1aa77-109">Select the user you would like to reset the password for.</span><span class="sxs-lookup"><span data-stu-id="1aa77-109">Select the user you would like to reset the password for.</span></span>
2. <span data-ttu-id="1aa77-110">For the selected user, select **Reset password**.</span><span class="sxs-lookup"><span data-stu-id="1aa77-110">For the selected user, select **Reset password**.</span></span>

    ![Reset a password for a user from the User profile in Azure AD](./media/active-directory-users-reset-password-azure-portal/user-password-reset.png)
    
6. <span data-ttu-id="1aa77-112">On **Reset password**, select **Reset password**.</span><span class="sxs-lookup"><span data-stu-id="1aa77-112">On **Reset password**, select **Reset password**.</span></span>
7. <span data-ttu-id="1aa77-113">A temporary password is displayed that you can then provide to the user.</span><span class="sxs-lookup"><span data-stu-id="1aa77-113">A temporary password is displayed that you can then provide to the user.</span></span> <span data-ttu-id="1aa77-114">The user will be asked to then change their password the next time they logon.</span><span class="sxs-lookup"><span data-stu-id="1aa77-114">The user will be asked to then change their password the next time they logon.</span></span> 

   > [!NOTE]
   > <span data-ttu-id="1aa77-115">This temporary password does not have an expiration time so it will be valid until they log in and are then are forced to change it.</span><span class="sxs-lookup"><span data-stu-id="1aa77-115">This temporary password does not have an expiration time so it will be valid until they log in and are then are forced to change it.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="1aa77-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="1aa77-116">Next steps</span></span>
* [<span data-ttu-id="1aa77-117">Add a user</span><span class="sxs-lookup"><span data-stu-id="1aa77-117">Add a user</span></span>](../add-users-azure-active-directory.md)
* [<span data-ttu-id="1aa77-118">Assign administrator roles to a user</span><span class="sxs-lookup"><span data-stu-id="1aa77-118">Assign administrator roles to a user</span></span>](active-directory-users-assign-role-azure-portal.md)
* [<span data-ttu-id="1aa77-119">Manage user profiles</span><span class="sxs-lookup"><span data-stu-id="1aa77-119">Manage user profiles</span></span>](active-directory-users-profile-azure-portal.md)
* [<span data-ttu-id="1aa77-120">Delete a user in Azure AD</span><span class="sxs-lookup"><span data-stu-id="1aa77-120">Delete a user in Azure AD</span></span>](../add-users-azure-active-directory.md)
