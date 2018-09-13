---
title: Restore or permanently remove a recently deleted user in Azure Active Directory | Microsoft Docs
description: How to restore a deleted user, view restorable users, or permanently delete a user in Azure Active Directory
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: fundamentals
ms.topic: quickstart
ms.date: 05/09/2018
ms.author: lizross
ms.reviewer: jeffsta
ms.custom: it-pro
ms.openlocfilehash: 6cd772638ed10e9cac52352e4b602d41a784bba0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866709"
---
# <a name="restore-a-deleted-user-in-azure-active-directory"></a>Restore a deleted user in Azure Active Directory

This article contains instructions to restore or permanently delete a previously deleted user. When you delete a user in the Azure Active Directory (Azure AD), the deleted user is retained for 30 days from the deletion date. During that time, the user and its properties can be restored. 

> [!WARNING]
> After it is permanently deleted, the user cannot be restored.

## <a name="how-to-restore-a-recently-deleted-user"></a>How to restore a recently deleted user
When a user is recently deleted, all directory information is preserved. If the user is restored, that information is restored as well.

1. In the [Azure AD admin center](https://aad.portal.azure.com), select **Users** &gt; **Deleted users**. 
2. Select one or more recently deleted users.
3. Select **Restore user**.

## <a name="how-to-permanently-delete-a-recently-deleted-user"></a>How to permanently delete a recently deleted user

1. In the [Azure AD admin center](https://aad.portal.azure.com), select **Users** &gt; **Deleted users**. 
2. Select one or more recently deleted users.
3. Select **Delete permanently**.

## <a name="required-permissions"></a>Required permissions
The following permissions are sufficient to restore a user.

Role | Permissions 
--------- | ---------
Company Administrator<p>Partner Tier1 Support<p>Partner Tier2 Support<p>User Account Administrator | Can restore deleted users 
Company Administrator<p>Partner Tier1 Support<p>Partner Tier2 Support<p>User Account Administrator | Can permanently delete users

## <a name="next-steps"></a>Next steps
These articles provide additional information on Azure Active Directory user management.

* [Quickstart: Add or delete users to Azure Active Directory](add-users-azure-active-directory.md)
* [Manage user profiles](active-directory-users-profile-azure-portal.md)
* [Add guest users from another directory](../b2b/what-is-b2b.md) 
* [Assign a user to a role in your Azure AD](active-directory-users-assign-role-azure-portal.md)
