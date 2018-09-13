---
title: Manage the groups your group belongs to in Azure Active Directory preview | Microsoft Docs
description: Groups can contain other groups in Azure Active Directory. Here's how to manage those memberships.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b0bc64ab2a7b9bc43dc48c116b5b3b0a6e0701ef
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554952"
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Manage to which groups a group belongs in your Azure Active Directory tenant
Groups can contain other groups in Azure Active Directory preview. [What's in the preview?](active-directory-preview-explainer.md) Here's how to manage those memberships.

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a>How do I find the groups my group is a member of?
1. Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.
2. Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.

   ![Opening user management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. On the **Users and groups** blade, select **All groups**.

   ![Opening the groups blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. On the **Users and groups - All groups** blade, select a group.
5. On the **Group - *groupname*** blade, select **Group memberships**.

   ![Opening the group memberships blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. To add your group as a member of another group, on the **Group - Group memberships** blade, select the **Add** command.
7. Select a group from the **Select Group** blade, and then select the **Select** button at the bottom of the blade. You can add your group to only one group at a time. The **User** box filters the display based on matching your entry to any part of a user or device name. No wildcard characters are accepted in that box.

   ![Add a group membership](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. To remove your group as a member of another group, on the **Group - Group memberships** blade, select a group.
9. On the ***groupname*** blade, select the **Remove** command, and confirm your choice at the prompt.

   ![remove membership command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. When you finish changing group memberships for your group, select **Save**.

## <a name="additional-information"></a>Additional information
These articles provide additional information on Azure Active Directory.

* [See existing groups](active-directory-groups-view-azure-portal.md)
* [Create a new group and adding members](active-directory-groups-create-azure-portal.md)
* [Manage settings of a group](active-directory-groups-settings-azure-portal.md)
* [Manage members of a group](active-directory-groups-members-azure-portal.md)
* [Manage dynamic rules for users in a group](active-directory-groups-dynamic-membership-azure-portal.md)





