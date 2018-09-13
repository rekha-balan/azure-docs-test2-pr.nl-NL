---
title: Change the name or logo of an enterprise app in Azure Active Directory preview | Microsoft Docs
description: How to change the name or logo for a custom enterprise app in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 0e4d6eff2a950e61be4551b675beedd299cf523b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540994"
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory-preview"></a>Change the name or logo of an enterprise app in Azure Active Directory preview
It's easy to change the name or logo for a custom enterprise application in Azure Active Directory (Azure AD) preview. [What's in the preview?](active-directory-preview-explainer.md) You must have the appropriate permissions to make these changes. In the current preview, you must be the creator of the custom app.

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a>How do I change an enterprise app's name or logo?
1. Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.
2. Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.
3. On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.

    ![Opening Enterprise apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. On the **Enterprise applications** blade, select **All applications**. You'll see a list of the apps you can manage.
5. On the **Enterprise applications - All applications** blade, select an app.
6. On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.

    ![Selecting the properties command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. On the ***appname*** **- Properties** blade, browse for a file to use as a new logo, or edit the app name, or both.

    ![Changing the app logo or nameproperties command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. Select the **Save** command.

## <a name="next-steps"></a>Next steps
* [See all of my groups](active-directory-groups-view-azure-portal.md)
* [Assign a user or group to an enterprise app](active-directory-coreapps-assign-user-azure-portal.md)
* [Remove a user or group assignment from an enterprise app](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Disable user sign-ins for an enterprise app](active-directory-coreapps-disable-app-azure-portal.md)



