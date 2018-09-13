---
title: How applications appear on the access panel | Microsoft Docs
description: Troubleshoot why an application is appearing in the Access Panel
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
ms.openlocfilehash: 2429ebef69aaddf28d10cd77bf4ce9072ea71476
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672174"
---
# <a name="how-applications-appear-on-the-access-panel"></a>How applications appear on the access panel

The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to. These applications are configured on behalf of the user in the Azure AD portal. The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.

## <a name="general-issues-to-check-first"></a>General issues to check first

-   If an application was just removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.

-   If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made. allow for extra time before signing into the Access Panel.

## <a name="problems-related-to-assigning-applications-to-users"></a>Problems related to assigning applications to users

A user may be seeing an application on their Access Panel because they had been previously assigned to it. Below are some ways to check:

-   [Check if a user is assigned to the application](#check-if-a-user-is-assigned-to-the-application)

-   [Check if a user is under a license related to the application](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-to-the-application"></a>Check if a user is assigned to the application

To check if a user is assigned to the application, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.

5.  click **All Applications** to view a list of all your applications.

6.  **Search** for the name of the application in question.

7.  click **Users and groups**.

8.  Check to see if your user is assigned to the application.

  * If you want to remove the user from the application, **click the row** of the user and select **delete**.

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a>Check if a user is under a license related to the application

To check a user’s assigned licenses, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All users**.

6.  **Search** for the user you are interested in and **click the row** to select.

7.  click **Licenses** to see which licenses the user currently has assigned.

   * If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.

## <a name="problems-related-to-assigning-applications-to-groups"></a>Problems related to assigning applications to groups

A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application. Below are some ways to check:

-   [Check a user’s group memberships](#check-a-users-group-memberships)

-   [Check if a user is a member of a group assigned to a license](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a>Check a user’s group memberships

To check a group’s membership, follow the steps below:

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All users**.

6.  **Search** for the user you are interested in and **click the row** to select.

7.  click **Groups.**

8.  Check to see if your user is part of a Group assigned to the application.

   * If you want to remove the user from the group, **click the row** of the group and select delete.

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-to-a-license"></a>Check if a user is a member of a group assigned to a license

1.  Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**

2.  Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.

3.  Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.

4.  click **Users and groups** in the navigation menu.

5.  click **All users**.

6.  **Search** for the user you are interested in and **click the row** to select.

7.  click **Groups.**

8.  click the row of a specific group.

9.  click **Licenses** to see which licenses the group has assigned to it.

  * If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.


## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a>If these troubleshooting steps do not the resolve the issue

open a support ticket with the following information if available:

-   Correlation error ID

-   UPN (user email address)

-   Tenant ID

-   Browser type

-   Time zone and time/timeframe during error occurs

-   Fiddler traces

## <a name="next-steps"></a>Next steps
[Managing Applications with Azure Active Directory](active-directory-enable-sso-scenario.md)
