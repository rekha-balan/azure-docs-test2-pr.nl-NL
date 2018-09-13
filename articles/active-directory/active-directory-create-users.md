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
# <a name="add-new-users--or-users-with-microsoft-accounts-to-azure-active-directory"></a>Add new users  or users with Microsoft accounts to Azure Active Directory
Add users to populate your directory. This article explains how to add new users in your organization, and how to add users who have Microsoft accounts. For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md). Added users don't have administrator permissions by default, but you can assign roles to them at any time.

## <a name="add-a-user"></a>Add a user
1. Sign in to the [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for the directory.
2. Select **Active Directory**, and then select the name of your organization directory.
3. Select the **Users** tab, and then, in the command bar, select **Add User**.
4. On the **Tell us about this user** page, under **Type of user**, select either:

   * **New user in your organization** – adds a new user account in your directory.
   * **User with an existing Microsoft account** – adds an existing Microsoft consumer account to your directory (for example, an Outlook account)
5. Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).
6. On the user **Profile** page, provide a first and last name, a user-friendly name, and a user role from the **Roles** list. For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md). Specify whether to **Enable Multi-Factor Authentication** for the user.
7. On the **Get temporary password** page, select **Create**.

> [!IMPORTANT]
> If your organization uses more than one domain, you should know about the following issues when you add a user account:
>
> * TO add user accounts with the same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.
> * **Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com. This order is important, and can be cumbersome to undo.
>
>

## <a name="change-user-information"></a>Change user information
You can change any user attribute except for the object ID.

1. Open your directory.
2. Select the **Users** tab, and then select the display name of the user you want to change.
3. Complete your changes, and then click **Save**.

If the user that you're changing is synchronized with your on-premises Active Directory service, you can't change the user information using this procedure. To change the user, use your on-premises Active Directory management tools.

## <a name="guest-user-management-and-limitations"></a>Guest user management and limitations
Guest accounts are users from other directories who were invited to your directory to access SharePoint documents, applications, or other Azure resources. A guest account in your directory has its underlying UserType attribute set to "Guest." Regular users (specifically, members of your directory) have the UserType attribute "Member."

Guests have a limited set of rights in the directory. These rights limit the ability for Guests to discover information about other users in the directory. However, guest users can still interact with the users and groups associated with the resources they're working on. Guest users can:

* See other users and groups associated with an Azure subscription to which they're assigned
* See the members of groups to which they belong
* Look up other users in the directory, if they know the full email address of the user
* See only a limited set of attributes of the users they look up--limited to display name, email address, user principal name (UPN), and thumbnail photo
* Get a list of verified domains in the directory
* Consent to applications, granting them the same access that Members have in your directory

## <a name="set-guest-user-access-policies"></a>Set guest user access policies
The **Configure** tab of a directory includes options to control access for guest users. These options can be changed only in Azure classic portal by a directory global administrator. Currently, there's no PowerShell or API method.

To open the **Configure** tab in the Azure classic portal, select **Active Directory**, and then select the name of the directory.

![Configure tab in Azure Active Directory][1]

Then you can edit the options to control access for guest users.

![access control options for guest users][2]

## <a name="whats-next"></a>What's next
* [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md)
* [Administering Azure AD](active-directory-administer.md)
* [Manage passwords in Azure AD](active-directory-manage-passwords.md)
* [Manage groups in Azure AD](active-directory-manage-groups.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-create-users/RBACDirConfigTab.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-create-users/RBACGuestAccessControls.png


