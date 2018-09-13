---
title: Create a group for users in Azure Active Directory preview | Microsoft Docs
description: How to create a group in Azure Active Directory and add members to the group
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 68e9b362b2db2f3911d4ca60c40d26bfbd80dac1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553748"
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>Create a group and add members in Azure Active Directory
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-groups-create-azure-portal.md)
> * [Azure classic portal](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

This article explains how to create and populate a new group in the Azure Active Directory (Azure AD) preview. [What's in the preview?](active-directory-preview-explainer.md) Use a group to perform management tasks such as assigning licenses or permissions to a number of users or devices at once.

## <a name="how-do-i-create-a-group"></a>How do I create a group?
1. Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.
2. Select **More services**, enter **User and groups** in the text box, and then select **Enter**.

   ![Opening user management](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-create-azure-portal/search-user-management.png)
3. On the **Users and groups** blade, select **All groups**.

   ![Opening the groups blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. On the **Users and groups - All groups** blade, select the **Add** command.

   ![Selecting the Add command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-create-azure-portal/add-group-command.png)
5. On the **Group** blade, add a name and description for the group.
6. To select members to add to the group, select **Assigned** in the **Membership type** box, and then select **Members**. For more information about how to manage the membership of a group dynamically, see [Using attributes to create advanced rules for group membership](active-directory-groups-dynamic-membership-azure-portal.md).

   ![Selecting members to add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-create-azure-portal/select-members.png)
7. On the **Members** blade, select one or more users or devices to add to the group and select the **Select** button at the bottom of the blade to add them to the group. The **User** box filters the display based on matching your entry to any part of a user or device name. No wildcard characters are accepted in that box.
8. When you finish adding members to the group, select **Create** on the **Group** blade.    

   ![Create group confirmation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-groups-create-azure-portal/create-group-confirmation.png)

## <a name="next-steps"></a>Next steps
These articles provide additional information on Azure Active Directory.

* [See existing groups](active-directory-groups-view-azure-portal.md)
* [Manage settings of a group](active-directory-groups-settings-azure-portal.md)
* [Manage members of a group](active-directory-groups-members-azure-portal.md)
* [Manage memberships of a group](active-directory-groups-membership-azure-portal.md)
* [Manage dynamic rules for users in a group](active-directory-groups-dynamic-membership-azure-portal.md)





