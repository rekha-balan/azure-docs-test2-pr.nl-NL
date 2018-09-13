---
title: Add new users to Azure Active Directory | Microsoft Docs
description: Explains how to add new users or change user information in Azure Active Directory.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/10/2017
ms.author: curtand
ms.openlocfilehash: c5211bbb9f18a1a724234011bc677260fa8b0eda
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550072"
---
# <a name="add-new-users--or-users-with-microsoft-accounts-to-azure-active-directory"></a><span data-ttu-id="4f4aa-103">Add new users  or users with Microsoft accounts to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f4aa-103">Add new users  or users with Microsoft accounts to Azure Active Directory</span></span>
<span data-ttu-id="4f4aa-104">Add users to populate your directory.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-104">Add users to populate your directory.</span></span> <span data-ttu-id="4f4aa-105">This article explains how to add new users in your organization, and how to add users who have Microsoft accounts.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-105">This article explains how to add new users in your organization, and how to add users who have Microsoft accounts.</span></span> <span data-ttu-id="4f4aa-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span><span class="sxs-lookup"><span data-stu-id="4f4aa-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="4f4aa-107">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-107">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

## <a name="add-a-user"></a><span data-ttu-id="4f4aa-108">Add a user</span><span class="sxs-lookup"><span data-stu-id="4f4aa-108">Add a user</span></span>
1. <span data-ttu-id="4f4aa-109">Sign in to the [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for the directory.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-109">Sign in to the [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="4f4aa-110">Select **Active Directory**, and then select the name of your organization directory.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-110">Select **Active Directory**, and then select the name of your organization directory.</span></span>
3. <span data-ttu-id="4f4aa-111">Select the **Users** tab, and then, in the command bar, select **Add User**.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-111">Select the **Users** tab, and then, in the command bar, select **Add User**.</span></span>
4. <span data-ttu-id="4f4aa-112">On the **Tell us about this user** page, under **Type of user**, select either:</span><span class="sxs-lookup"><span data-stu-id="4f4aa-112">On the **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="4f4aa-113">**New user in your organization** – adds a new user account in your directory.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-113">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="4f4aa-114">**User with an existing Microsoft account** – adds an existing Microsoft consumer account to your directory (for example, an Outlook account)</span><span class="sxs-lookup"><span data-stu-id="4f4aa-114">**User with an existing Microsoft account** – adds an existing Microsoft consumer account to your directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="4f4aa-115">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span><span class="sxs-lookup"><span data-stu-id="4f4aa-115">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="4f4aa-116">On the user **Profile** page, provide a first and last name, a user-friendly name, and a user role from the **Roles** list.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-116">On the user **Profile** page, provide a first and last name, a user-friendly name, and a user role from the **Roles** list.</span></span> <span data-ttu-id="4f4aa-117">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4f4aa-117">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="4f4aa-118">Specify whether to **Enable Multi-Factor Authentication** for the user.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-118">Specify whether to **Enable Multi-Factor Authentication** for the user.</span></span>
7. <span data-ttu-id="4f4aa-119">On the **Get temporary password** page, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-119">On the **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f4aa-120">If your organization uses more than one domain, you should know about the following issues when you add a user account:</span><span class="sxs-lookup"><span data-stu-id="4f4aa-120">If your organization uses more than one domain, you should know about the following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="4f4aa-121">TO add user accounts with the same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-121">TO add user accounts with the same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="4f4aa-122">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-122">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span></span> <span data-ttu-id="4f4aa-123">This order is important, and can be cumbersome to undo.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-123">This order is important, and can be cumbersome to undo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="4f4aa-124">Change user information</span><span class="sxs-lookup"><span data-stu-id="4f4aa-124">Change user information</span></span>
<span data-ttu-id="4f4aa-125">You can change any user attribute except for the object ID.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-125">You can change any user attribute except for the object ID.</span></span>

1. <span data-ttu-id="4f4aa-126">Open your directory.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-126">Open your directory.</span></span>
2. <span data-ttu-id="4f4aa-127">Select the **Users** tab, and then select the display name of the user you want to change.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-127">Select the **Users** tab, and then select the display name of the user you want to change.</span></span>
3. <span data-ttu-id="4f4aa-128">Complete your changes, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-128">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="4f4aa-129">If the user that you're changing is synchronized with your on-premises Active Directory service, you can't change the user information using this procedure.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-129">If the user that you're changing is synchronized with your on-premises Active Directory service, you can't change the user information using this procedure.</span></span> <span data-ttu-id="4f4aa-130">To change the user, use your on-premises Active Directory management tools.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-130">To change the user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="4f4aa-131">Guest user management and limitations</span><span class="sxs-lookup"><span data-stu-id="4f4aa-131">Guest user management and limitations</span></span>
<span data-ttu-id="4f4aa-132">Guest accounts are users from other directories who were invited to your directory to access SharePoint documents, applications, or other Azure resources.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-132">Guest accounts are users from other directories who were invited to your directory to access SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="4f4aa-133">A guest account in your directory has its underlying UserType attribute set to "Guest."</span><span class="sxs-lookup"><span data-stu-id="4f4aa-133">A guest account in your directory has its underlying UserType attribute set to "Guest."</span></span> <span data-ttu-id="4f4aa-134">Regular users (specifically, members of your directory) have the UserType attribute "Member."</span><span class="sxs-lookup"><span data-stu-id="4f4aa-134">Regular users (specifically, members of your directory) have the UserType attribute "Member."</span></span>

<span data-ttu-id="4f4aa-135">Guests have a limited set of rights in the directory.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-135">Guests have a limited set of rights in the directory.</span></span> <span data-ttu-id="4f4aa-136">These rights limit the ability for Guests to discover information about other users in the directory.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-136">These rights limit the ability for Guests to discover information about other users in the directory.</span></span> <span data-ttu-id="4f4aa-137">However, guest users can still interact with the users and groups associated with the resources they're working on.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-137">However, guest users can still interact with the users and groups associated with the resources they're working on.</span></span> <span data-ttu-id="4f4aa-138">Guest users can:</span><span class="sxs-lookup"><span data-stu-id="4f4aa-138">Guest users can:</span></span>

* <span data-ttu-id="4f4aa-139">See other users and groups associated with an Azure subscription to which they're assigned</span><span class="sxs-lookup"><span data-stu-id="4f4aa-139">See other users and groups associated with an Azure subscription to which they're assigned</span></span>
* <span data-ttu-id="4f4aa-140">See the members of groups to which they belong</span><span class="sxs-lookup"><span data-stu-id="4f4aa-140">See the members of groups to which they belong</span></span>
* <span data-ttu-id="4f4aa-141">Look up other users in the directory, if they know the full email address of the user</span><span class="sxs-lookup"><span data-stu-id="4f4aa-141">Look up other users in the directory, if they know the full email address of the user</span></span>
* <span data-ttu-id="4f4aa-142">See only a limited set of attributes of the users they look up--limited to display name, email address, user principal name (UPN), and thumbnail photo</span><span class="sxs-lookup"><span data-stu-id="4f4aa-142">See only a limited set of attributes of the users they look up--limited to display name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="4f4aa-143">Get a list of verified domains in the directory</span><span class="sxs-lookup"><span data-stu-id="4f4aa-143">Get a list of verified domains in the directory</span></span>
* <span data-ttu-id="4f4aa-144">Consent to applications, granting them the same access that Members have in your directory</span><span class="sxs-lookup"><span data-stu-id="4f4aa-144">Consent to applications, granting them the same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="4f4aa-145">Set guest user access policies</span><span class="sxs-lookup"><span data-stu-id="4f4aa-145">Set guest user access policies</span></span>
<span data-ttu-id="4f4aa-146">The **Configure** tab of a directory includes options to control access for guest users.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-146">The **Configure** tab of a directory includes options to control access for guest users.</span></span> <span data-ttu-id="4f4aa-147">These options can be changed only in Azure classic portal by a directory global administrator.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-147">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="4f4aa-148">Currently, there's no PowerShell or API method.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-148">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="4f4aa-149">To open the **Configure** tab in the Azure classic portal, select **Active Directory**, and then select the name of the directory.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-149">To open the **Configure** tab in the Azure classic portal, select **Active Directory**, and then select the name of the directory.</span></span>

![Configure tab in Azure Active Directory][1]

<span data-ttu-id="4f4aa-151">Then you can edit the options to control access for guest users.</span><span class="sxs-lookup"><span data-stu-id="4f4aa-151">Then you can edit the options to control access for guest users.</span></span>

![access control options for guest users][2]

## <a name="whats-next"></a><span data-ttu-id="4f4aa-153">What's next</span><span class="sxs-lookup"><span data-stu-id="4f4aa-153">What's next</span></span>
* [<span data-ttu-id="4f4aa-154">Add users from other directories or partner companies in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f4aa-154">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="4f4aa-155">Administering Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f4aa-155">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="4f4aa-156">Manage passwords in Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f4aa-156">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="4f4aa-157">Manage groups in Azure AD</span><span class="sxs-lookup"><span data-stu-id="4f4aa-157">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-create-users/RBACDirConfigTab.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-create-users/RBACGuestAccessControls.png


