---
title: Using a group to manage access to SaaS Applications | Microsoft Docs
description: How to use groups in Azure Active Directory Premium or Basic to assign access to SaaS applications that are integrated with Azure Active Directory.
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 03/14/2017
ms.author: curtand
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 8c04f2723466ea7abc8ea3c3cc1f1efb953da764
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969326"
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a>Using a group to manage access to SaaS applications
Using Azure Active Directory (Azure AD) with an Azure AD Premium or Azure AD Basic license, you can use groups to assign access to a SaaS application that's integrated with Azure AD. For example, if you want to assign access for the marketing department to use five different SaaS applications, you can create a group that contains the users in the marketing department, and then assign that group to these five SaaS applications that are needed by the marketing department. This way you can save time by managing the membership of the marketing department in one place. Users then are assigned to the application when they are added as members of the marketing group, and have their assignments removed from the application when they are removed from the marketing group. This capability can be used with hundreds of applications that you can add from within the Azure AD Application Gallery.

> [!IMPORTANT]
> You can use this feature only after you start an Azure AD Premium trial or purchase Azure AD Premium or Azure AD Basic licenses. Group-based assignment is supported only for Security groups. Nested group memberships are not supported for group-based assignment to applications at this time.

**To assign access for a user or group to a SaaS application**

1. In the [Azure AD admin center](https://aad.portal.azure.com), select **Enterprise applications**.
2. Select an application that you added from the Application Gallery to open it.
3. Select **Users and groups**, and then select **Add user**.
4. On **Add Assignment**, select **Users and groups** to open the **Users and groups** selection list.
6. Select as many groups or users as you want, then click or tap **Select** to add them to the **Add Assignment** list. You can also assign a role to a user at this stage.
7. Select **Assign** to assign the users or groups to the selected enterprise application.

### <a name="next-steps"></a>Next steps
These articles provide additional information on Azure Active Directory.

* [Managing access to resources with Azure Active Directory groups](../fundamentals/active-directory-manage-groups.md)
* [Article Index for Application Management in Azure Active Directory](../active-directory-apps-index.md)
* [Azure Active Directory cmdlets for configuring group settings](groups-settings-cmdlets.md)
* [What is Azure Active Directory?](../fundamentals/active-directory-whatis.md)
* [Integrating your on-premises identities with Azure Active Directory](../connect/active-directory-aadconnect.md)