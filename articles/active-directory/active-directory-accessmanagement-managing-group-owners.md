---
title: Next steps for access management using groups | Microsoft Docs
description: Advanced How-to's for managing security groups and how to use these groups to manage access to a resource.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: curtand
ms.openlocfilehash: aaf064b6c7db86f287ac50e4e381e661297c1e37
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662183"
---
# <a name="managing-owners-for-a-group"></a>Managing owners for a group
Once a resource owner has assigned access to a resource to an Azure AD group, the membership of the group is managed by the group owner. The resource owner effectively delegates the permission to assign users to the resource to the owner of the group.

## <a name="assigning-group-ownership"></a>Assigning group ownership
**To add an owner to a group**

1. In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.
2. Select the **Groups** tab, and then open the group that you want to add owners to.
3. Select **Add Owners**.
4. On the **Add owners** page, select the user that you want to add as the owner of this group, and make sure this name is added to the **Selected** pane.

**To remove an owner from a group**

1. In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then open your organization’s directory.
2. Select the **Groups** tab, and then open the group that you want to remove an owner from.
3. Select the **Owners** tab.
4. Select the owner that you want to remove from this group, and then select **Remove**.

## <a name="additional-information"></a>Additional information
These articles provide additional information on Azure Active Directory.

* [Managing access to resources with Azure Active Directory groups](active-directory-manage-groups.md)
* [Azure Active Directory cmdlets for configuring group settings](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)
* [What is Azure Active Directory?](active-directory-whatis.md)
* [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md)
