---
title: Disable user sign-ins for an enterprise app in Azure Active Directory preview | Microsoft Docs
description: How to disable an enterprise application so that no users may sign in to it in Azure Active Directory
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 9d3b7f6b52c575e7beb0c5ca4f0d35dc1cbf1dc6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553976"
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory-preview"></a>Disable user sign-ins for an enterprise app in Azure Active Directory preview
It's easy to disable an enterprise application so that no users may sign in to it in Azure Active Directory (Azure AD) preview. [What's in the preview?](active-directory-preview-explainer.md) You must have the appropriate permissions to manage the enterprise app. In the current preview, you must be global admin for the directory.

## <a name="how-do-i-disable-user-sign-ins"></a>How do I disable user sign-ins?
1. Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.
2. Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.
3. On the **Azure Active Directory** -  ***directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.

    ![Opening Enterprise apps](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. On the **Enterprise applications** blade, select **All applications**. You see a list of the apps you can manage.
5. On the **Enterprise applications - All applications** blade, select an app.
6. On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Properties**.

    ![Selecting the all applications command](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. On the ***appname*** - **Properties** blade, select **No** for **Enabled for users to sign-in?**.
8. Select the **Save** command.

## <a name="next-steps"></a>Next steps
* [See all my groups](active-directory-groups-view-azure-portal.md)
* [Assign a user or group to an enterprise app](active-directory-coreapps-assign-user-azure-portal.md)
* [Remove a user or group assignment from an enterprise app](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Change the name or logo of an enterprise app](active-directory-coreapps-change-app-logo-user-azure-portal.md)


