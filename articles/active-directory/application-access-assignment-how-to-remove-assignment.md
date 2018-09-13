---
title: How to remove a user's access to an application | Microsoft Docs
description: Understand how to remove a user's access to an application
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: 8d4f2cec35a8edfec9b8830a077b8aa65ca0c229
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552611"
---
# <a name="how-to-remove-a-users-access-to-an-application"></a>How to remove a user's access to an application

This article help you to understand how to remove a user's access to an application.

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a>I want to remove a specific user’s or group’s assignment to an application

To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.

.## I want to disable all access to an application for every user

To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.

## <a name="i-want-to-delete-an-application-entirely"></a>I want to delete an application entirely

To **delete an application**, follow the instructions below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  Click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.

5.  Click **All Applications** to view a list of all your applications.

   * If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**

6.  Select the application you want to delete.

7.  Once the application loads, click **Delete** icon from the top application’s **Overview** blade.

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a>I want to disable all future user consent operations to any application

Disabling user consent for your entire directory prevent end users from consenting to any application. Administrators can still consent on user’s behalves. To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

To **disable all future user consent operations in your entire directory**, follow the instructions below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  Click **Users and groups** in the navigation menu.

5.  Click **User settings**.

6.  Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.


# <a name="next-steps"></a>Next steps
[Managing access to apps](active-directory-managing-access-to-apps.md)
