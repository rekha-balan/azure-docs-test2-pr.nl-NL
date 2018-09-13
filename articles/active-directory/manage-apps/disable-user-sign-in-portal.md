---
title: Disable user sign-ins for an enterprise app in Azure Active Directory | Microsoft Docs
description: How to disable an enterprise application so that no users may sign in to it in Azure Active Directory
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/28/2017
ms.author: barbkess
ms.reviewer: asteen
ms.custom: it-pro
ms.openlocfilehash: 39e926a392cbd87eff23e25d9708792ec7c40a2c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868047"
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a>Disable user sign-ins for an enterprise app in Azure Active Directory
It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD). You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.

## <a name="how-do-i-disable-user-sign-ins"></a>How do I disable user sign-ins?
1. Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.
2. Select **All services**, enter **Azure Active Directory** in the text box, and then select **Enter**.
3. On the **Azure Active Directory** -  ***directoryname*** pane (that is, the Azure AD pane for the directory you are managing), select **Enterprise applications**.

    ![Opening Enterprise apps](./media/disable-user-sign-in-portal/open-enterprise-apps.png)
4. On the **Enterprise applications** pane, select **All applications**. You see a list of the apps you can manage.
5. On the **Enterprise applications - All applications** pane, select an app.
6. On the ***appname*** pane (that is, the pane with the name of the selected app in the title), select **Properties**.

    ![Selecting the all applications command](./media/disable-user-sign-in-portal/select-app.png)
7. On the ***appname*** - **Properties** pane, select **No** for **Enabled for users to sign-in?**.
8. Select the **Save** command.

## <a name="next-steps"></a>Next steps
* [See all my groups](../fundamentals/active-directory-groups-view-azure-portal.md)
* [Assign a user or group to an enterprise app](assign-user-or-group-access-portal.md)
* [Remove a user or group assignment from an enterprise app](remove-user-or-group-access-portal.md)
* [Change the name or logo of an enterprise app](change-name-or-logo-portal.md)
