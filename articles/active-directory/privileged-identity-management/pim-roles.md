---
title: Azure AD directory roles you can manage in PIM | Microsoft Docs
description: Describes the Azure AD directory roles you can manage in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: pim
ms.date: 07/23/2018
ms.author: rolyon
ms.custom: pim ; H1Hack27Feb2017;oldportal;it-pro;
ms.openlocfilehash: cf0c9b76a7edace9f2a9147823b292e218e20bf7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857345"
---
# <a name="azure-ad-directory-roles-you-can-manage-in-pim"></a><span data-ttu-id="8926e-103">Azure AD directory roles you can manage in PIM</span><span class="sxs-lookup"><span data-stu-id="8926e-103">Azure AD directory roles you can manage in PIM</span></span>
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

<span data-ttu-id="8926e-104">You can assign users in your organization to different administrative roles in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8926e-104">You can assign users in your organization to different administrative roles in Azure AD.</span></span> <span data-ttu-id="8926e-105">These role assignments control which tasks, such as adding or removing users or changing service settings, the users are able to perform on Azure AD, Office 365, and other Microsoft Online Services and connected applications.</span><span class="sxs-lookup"><span data-stu-id="8926e-105">These role assignments control which tasks, such as adding or removing users or changing service settings, the users are able to perform on Azure AD, Office 365, and other Microsoft Online Services and connected applications.</span></span>  

<span data-ttu-id="8926e-106">A Global Administrator can update which users are **permanently** assigned to roles in Azure AD through the portal as described in [assigning administrator roles in Azure Active Directory](../users-groups-roles/directory-assign-admin-roles.md) or using [PowerShell commands](/powershell/module/azuread#directory_roles).</span><span class="sxs-lookup"><span data-stu-id="8926e-106">A Global Administrator can update which users are **permanently** assigned to roles in Azure AD through the portal as described in [assigning administrator roles in Azure Active Directory](../users-groups-roles/directory-assign-admin-roles.md) or using [PowerShell commands](/powershell/module/azuread#directory_roles).</span></span>

<span data-ttu-id="8926e-107">Azure AD Privileged Identity Management (PIM) manages policies for privileged access for users in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8926e-107">Azure AD Privileged Identity Management (PIM) manages policies for privileged access for users in Azure AD.</span></span> <span data-ttu-id="8926e-108">PIM assigns users to one or more roles in Azure AD, and you can assign someone to be permanently in the role, or eligible for the role.</span><span class="sxs-lookup"><span data-stu-id="8926e-108">PIM assigns users to one or more roles in Azure AD, and you can assign someone to be permanently in the role, or eligible for the role.</span></span> <span data-ttu-id="8926e-109">When a user is permanently assigned to a role, or activates an eligible role assignment, then they can manage Azure Active Directory, Office 365, and other applications with the permissions assigned to their roles.</span><span class="sxs-lookup"><span data-stu-id="8926e-109">When a user is permanently assigned to a role, or activates an eligible role assignment, then they can manage Azure Active Directory, Office 365, and other applications with the permissions assigned to their roles.</span></span>

<span data-ttu-id="8926e-110">There's no difference in the access given to someone with a permanent versus an eligible role assignment.</span><span class="sxs-lookup"><span data-stu-id="8926e-110">There's no difference in the access given to someone with a permanent versus an eligible role assignment.</span></span> <span data-ttu-id="8926e-111">The only difference is that some people don't need that access all the time.</span><span class="sxs-lookup"><span data-stu-id="8926e-111">The only difference is that some people don't need that access all the time.</span></span> <span data-ttu-id="8926e-112">They are made eligible for the role, and can turn it on and off whenever they need to.</span><span class="sxs-lookup"><span data-stu-id="8926e-112">They are made eligible for the role, and can turn it on and off whenever they need to.</span></span>

## <a name="roles-managed-in-pim"></a><span data-ttu-id="8926e-113">Roles managed in PIM</span><span class="sxs-lookup"><span data-stu-id="8926e-113">Roles managed in PIM</span></span>
<span data-ttu-id="8926e-114">Privileged Identity Management lets you assign users to common administrator roles, including:</span><span class="sxs-lookup"><span data-stu-id="8926e-114">Privileged Identity Management lets you assign users to common administrator roles, including:</span></span>

* <span data-ttu-id="8926e-115">**Global administrator** (also known as Company administrator) has access to all administrative features.</span><span class="sxs-lookup"><span data-stu-id="8926e-115">**Global administrator** (also known as Company administrator) has access to all administrative features.</span></span> <span data-ttu-id="8926e-116">You can have more than one global admin in your organization.</span><span class="sxs-lookup"><span data-stu-id="8926e-116">You can have more than one global admin in your organization.</span></span> <span data-ttu-id="8926e-117">The person who signs up to purchase Office 365 automatically becomes a global admin.</span><span class="sxs-lookup"><span data-stu-id="8926e-117">The person who signs up to purchase Office 365 automatically becomes a global admin.</span></span>
* <span data-ttu-id="8926e-118">**Privileged role administrator** manages Azure AD PIM and updates role assignments for other users.</span><span class="sxs-lookup"><span data-stu-id="8926e-118">**Privileged role administrator** manages Azure AD PIM and updates role assignments for other users.</span></span>  
* <span data-ttu-id="8926e-119">**Billing administrator** makes purchases, manages subscriptions, manages support tickets, and monitors service health.</span><span class="sxs-lookup"><span data-stu-id="8926e-119">**Billing administrator** makes purchases, manages subscriptions, manages support tickets, and monitors service health.</span></span>
* <span data-ttu-id="8926e-120">**Password administrator** resets passwords, manages service requests, and monitors service health.</span><span class="sxs-lookup"><span data-stu-id="8926e-120">**Password administrator** resets passwords, manages service requests, and monitors service health.</span></span> <span data-ttu-id="8926e-121">Password admins are limited to resetting passwords for users.</span><span class="sxs-lookup"><span data-stu-id="8926e-121">Password admins are limited to resetting passwords for users.</span></span>
* <span data-ttu-id="8926e-122">**Service administrator** manages service requests and monitors service health.</span><span class="sxs-lookup"><span data-stu-id="8926e-122">**Service administrator** manages service requests and monitors service health.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="8926e-123">If you are using Office 365, then before assigning the service admin role to a user, first assign the user administrative permissions to a service, such as Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="8926e-123">If you are using Office 365, then before assigning the service admin role to a user, first assign the user administrative permissions to a service, such as Exchange Online.</span></span>
  > 
  > 
* <span data-ttu-id="8926e-124">**User management administrator** resets passwords, monitors service health, and manages user accounts, user groups, and service requests.</span><span class="sxs-lookup"><span data-stu-id="8926e-124">**User management administrator** resets passwords, monitors service health, and manages user accounts, user groups, and service requests.</span></span> <span data-ttu-id="8926e-125">The user management admin can’t delete a global admin, create other admin roles, or reset passwords for billing, global, and service admins.</span><span class="sxs-lookup"><span data-stu-id="8926e-125">The user management admin can’t delete a global admin, create other admin roles, or reset passwords for billing, global, and service admins.</span></span>
* <span data-ttu-id="8926e-126">**Exchange administrator** has administrative access to Exchange Online through the Exchange admin center (EAC), and can perform almost any task in Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="8926e-126">**Exchange administrator** has administrative access to Exchange Online through the Exchange admin center (EAC), and can perform almost any task in Exchange Online.</span></span>
* <span data-ttu-id="8926e-127">**SharePoint administrator (Preview)** has administrative access to SharePoint Online through the SharePoint Online admin center, and can perform almost any task in SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="8926e-127">**SharePoint administrator (Preview)** has administrative access to SharePoint Online through the SharePoint Online admin center, and can perform almost any task in SharePoint Online.</span></span> <span data-ttu-id="8926e-128">This role is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="8926e-128">This role is currently in preview.</span></span> <span data-ttu-id="8926e-129">Eligible users may experience delays using this role within SharePoint after activating in PIM.</span><span class="sxs-lookup"><span data-stu-id="8926e-129">Eligible users may experience delays using this role within SharePoint after activating in PIM.</span></span>
* <span data-ttu-id="8926e-130">**Skype for Business administrator** has administrative access to Skype for Business through the Skype for Business admin center, and can perform almost any task in Skype for Business Online.</span><span class="sxs-lookup"><span data-stu-id="8926e-130">**Skype for Business administrator** has administrative access to Skype for Business through the Skype for Business admin center, and can perform almost any task in Skype for Business Online.</span></span>

<span data-ttu-id="8926e-131">Read these articles for more details about [assigning administrator roles in Azure AD](../users-groups-roles/directory-assign-admin-roles.md) and [assigning admin roles in Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).</span><span class="sxs-lookup"><span data-stu-id="8926e-131">Read these articles for more details about [assigning administrator roles in Azure AD](../users-groups-roles/directory-assign-admin-roles.md) and [assigning admin roles in Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).</span></span>

<!--**PLACEHOLDER: The above article may not be the one we want since PIM gets roles from places other that Office 365**-->


<span data-ttu-id="8926e-132">From PIM, you can [assign these roles to a user](pim-how-to-add-role-to-user.md) so that the user can [activate the role when needed](pim-how-to-activate-role.md).</span><span class="sxs-lookup"><span data-stu-id="8926e-132">From PIM, you can [assign these roles to a user](pim-how-to-add-role-to-user.md) so that the user can [activate the role when needed](pim-how-to-activate-role.md).</span></span>

<span data-ttu-id="8926e-133">If you want to give another user access to manage in PIM itself, the roles which PIM requires the user to have are described further in [how to give access to PIM](pim-how-to-give-access-to-pim.md).</span><span class="sxs-lookup"><span data-stu-id="8926e-133">If you want to give another user access to manage in PIM itself, the roles which PIM requires the user to have are described further in [how to give access to PIM](pim-how-to-give-access-to-pim.md).</span></span>

<!-- ## The PIM Security Administrator Role **PLACEHOLDER: Need description of the Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a><span data-ttu-id="8926e-134">Roles not managed in PIM</span><span class="sxs-lookup"><span data-stu-id="8926e-134">Roles not managed in PIM</span></span>
<span data-ttu-id="8926e-135">Roles within Exchange Online or SharePoint Online, except for those mentioned above, are not represented in Azure AD and so are not visible in PIM.</span><span class="sxs-lookup"><span data-stu-id="8926e-135">Roles within Exchange Online or SharePoint Online, except for those mentioned above, are not represented in Azure AD and so are not visible in PIM.</span></span> <span data-ttu-id="8926e-136">For more information on changing fine-grained role assignments in these Office 365 services, see [Permissions in Office 365](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).</span><span class="sxs-lookup"><span data-stu-id="8926e-136">For more information on changing fine-grained role assignments in these Office 365 services, see [Permissions in Office 365](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).</span></span>

<!--**The above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a><span data-ttu-id="8926e-137">User roles and signing in</span><span class="sxs-lookup"><span data-stu-id="8926e-137">User roles and signing in</span></span>
<span data-ttu-id="8926e-138">For some Microsoft services and applications, assigning a user to a role may not be sufficient to enable that user to be an administrator.</span><span class="sxs-lookup"><span data-stu-id="8926e-138">For some Microsoft services and applications, assigning a user to a role may not be sufficient to enable that user to be an administrator.</span></span>

<span data-ttu-id="8926e-139">Access to the Azure portal requires the user be an Owner of an Azure subscription, even if the user does not need to manage the Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8926e-139">Access to the Azure portal requires the user be an Owner of an Azure subscription, even if the user does not need to manage the Azure subscriptions.</span></span>  <span data-ttu-id="8926e-140">For example, to manage configuration settings for Azure AD, a user must be both a Global Administrator in Azure AD and an Owner on an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8926e-140">For example, to manage configuration settings for Azure AD, a user must be both a Global Administrator in Azure AD and an Owner on an Azure subscription.</span></span>  <span data-ttu-id="8926e-141">To learn how to add users to Azure subscriptions, see [Manage access using RBAC and the Azure portal](../..//role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8926e-141">To learn how to add users to Azure subscriptions, see [Manage access using RBAC and the Azure portal](../..//role-based-access-control/role-assignments-portal.md).</span></span>

<span data-ttu-id="8926e-142">Access to Microsoft Online Services may require the user also be assigned a license before they can open the service's portal or perform administrative tasks.</span><span class="sxs-lookup"><span data-stu-id="8926e-142">Access to Microsoft Online Services may require the user also be assigned a license before they can open the service's portal or perform administrative tasks.</span></span>

## <a name="assign-a-license-to-a-user-in-azure-ad"></a><span data-ttu-id="8926e-143">Assign a license to a user in Azure AD</span><span class="sxs-lookup"><span data-stu-id="8926e-143">Assign a license to a user in Azure AD</span></span>

1. <span data-ttu-id="8926e-144">Sign in to the [Azure portal](http://portal.azure.com) with a Global Administrator or Owner role.</span><span class="sxs-lookup"><span data-stu-id="8926e-144">Sign in to the [Azure portal](http://portal.azure.com) with a Global Administrator or Owner role.</span></span>

1. <span data-ttu-id="8926e-145">Select the Azure AD directory you want to work with and that has licenses associated with it.</span><span class="sxs-lookup"><span data-stu-id="8926e-145">Select the Azure AD directory you want to work with and that has licenses associated with it.</span></span>

1. <span data-ttu-id="8926e-146">In the left navigation, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8926e-146">In the left navigation, click **Azure Active Directory**.</span></span>

1. <span data-ttu-id="8926e-147">Click **Licenses**.</span><span class="sxs-lookup"><span data-stu-id="8926e-147">Click **Licenses**.</span></span> <span data-ttu-id="8926e-148">The list of available licenses will appear.</span><span class="sxs-lookup"><span data-stu-id="8926e-148">The list of available licenses will appear.</span></span>

    ![Azure Active Directory Licenses](./media/pim-roles/licenses-overview.png)

1. <span data-ttu-id="8926e-150">Click your **Product**.</span><span class="sxs-lookup"><span data-stu-id="8926e-150">Click your **Product**.</span></span>

1. <span data-ttu-id="8926e-151">Click the license plan that contains the licenses you want to distribute.</span><span class="sxs-lookup"><span data-stu-id="8926e-151">Click the license plan that contains the licenses you want to distribute.</span></span>

    ![Licenses Products](./media/pim-roles/licenses-products.png)

1. <span data-ttu-id="8926e-153">Click **Assign** to open the Assign license pane.</span><span class="sxs-lookup"><span data-stu-id="8926e-153">Click **Assign** to open the Assign license pane.</span></span>

    ![Licensed users](./media/pim-roles/licenses-licensed-users.png)

1. <span data-ttu-id="8926e-155">Select the user or group that you want to assign a license to.</span><span class="sxs-lookup"><span data-stu-id="8926e-155">Select the user or group that you want to assign a license to.</span></span>

    ![Assign license](./media/pim-roles/licenses-assign-license.png)

1. <span data-ttu-id="8926e-157">Click **Assignment options** to configure your assignment options.</span><span class="sxs-lookup"><span data-stu-id="8926e-157">Click **Assignment options** to configure your assignment options.</span></span>

    ![Assignment options](./media/pim-roles/licenses-assignment-options.png)

1. <span data-ttu-id="8926e-159">Click **Assign** to assign the license.</span><span class="sxs-lookup"><span data-stu-id="8926e-159">Click **Assign** to assign the license.</span></span> <span data-ttu-id="8926e-160">The user now has the license.</span><span class="sxs-lookup"><span data-stu-id="8926e-160">The user now has the license.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="8926e-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="8926e-161">Next steps</span></span>

- [<span data-ttu-id="8926e-162">Start using PIM</span><span class="sxs-lookup"><span data-stu-id="8926e-162">Start using PIM</span></span>](pim-getting-started.md)
- [<span data-ttu-id="8926e-163">Assign Azure AD directory roles in PIM</span><span class="sxs-lookup"><span data-stu-id="8926e-163">Assign Azure AD directory roles in PIM</span></span>](pim-how-to-add-role-to-user.md)

