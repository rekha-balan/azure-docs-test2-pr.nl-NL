---
title: Manage the members for a group in Azure Active Directory preview | Microsoft Docs
description: How to add or remove users and devices from a group in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c488d6c77f100b1f782d61e3fb9bbf04ed418ecb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554488"
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a>Manage group membership for users in your Azure Active Directory tenant
This article explains how to manage the members for a group in Azure Active Directory (Azure AD) preview. [What's in the preview?](active-directory-preview-explainer.md)

## <a name="how-do-i-find-the-members-and-manage-them"></a>How do I find the members and manage them?
1. Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.
2. Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.

   ![Opening user management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-members-azure-portal/search-user-management.png)
3. On the **Users and groups** blade, select **All groups**.

   ![Opening the groups blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. On the **Users and groups - All groups** blade, select a group.
5. On the **Group - *groupname*** blade, select **Members**.

   ![Opening the Members blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-members-azure-portal/view-group-members.png)
6. To add members to the group, on the **Group - Members** blade, select **Add Members**.

   ![Add Members command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group. The **User** box filters the display based on matching your entry to any part of a user or device name. No wildcard characters are accepted in that box.
8. To remove members from the group, on the **Group - Members** blade, select a member.
9. On the ***membername*** blade, select the **Remove** command, and confirm your choice at the prompt.

   ![remove Members command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. When you finish changing members for the group, select **Save**.

## <a name="additional-information"></a>Additional information
These articles provide additional information on Azure Active Directory.

* [See existing groups](active-directory-groups-view-azure-portal.md)
* [Create a new group and adding members](active-directory-groups-create-azure-portal.md)
* [Manage settings of a group](active-directory-groups-settings-azure-portal.md)
* [Manage memberships of a group](active-directory-groups-membership-azure-portal.md)
* [Manage dynamic rules for users in a group](active-directory-groups-dynamic-membership-azure-portal.md)





