---
title: Assign licenses to a group in Azure Active Directory | Microsoft Docs
description: How to assign licenses by using Azure Active Directory group-based licensing
services: active-directory
keywords: Azure AD licensing
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: ''
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf3df2bcdab0dfc8809c15b35abe845cb0289000
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554524"
---
# <a name="assign-licenses-to-a-group-of-users-in-azure-active-directory"></a>Assign licenses to a group of users in Azure Active Directory

In this article, we're going to walk through a basic scenario of assigning product licenses to a group of users in Azure Active Directory (Azure AD), and then verifying that all members of the group are correctly licensed.

In this example, the tenant contains a security group called *HR Department*. This group includes all members of the human resources department (in this case, around 1,000 users). The administrator wants to assign Office 365 Enterprise E3 licenses to the entire department. The Yammer Enterprise service that's included in the product needs to be temporarily disabled until a later time when the department is ready to start using it. The admin also wants to deploy Enterprise Mobility + Security licenses to the same group of users.

## <a name="step-1-assign-the-required-licenses"></a>Step 1: Assign the required licenses

1. Sign in to the [**Azure portal**](https://portal.azure.com) with an administrator account. For you to be able to manage licenses, the account needs either the Global Administrator role or the User Account Administrator role.

2. Select **More services** in the left navigation pane, and then select **Azure Active Directory**. You can “favorite” this blade by clicking the star icon or by pinning it to the portal dashboard.

3. On the **Azure Active Directory** blade, select **Licenses**. This opens a blade where you can see and manage all licensable products in the tenant.

4. Under **All products**, select both Office 365 Enterprise E3 and Enterprise Mobility + Security by selecting the product names. Select **Assign** at the top of the blade to start the assignment.

  ![All products, assign license](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-assignment-azure-portal/all-products-assign.png)

5. On the **Assign license** blade, click **Users and groups** to open the **Users and groups** blade. Search for the group name *HR Department*, select the group, and then be sure to confirm by clicking **Select** at the bottom of the blade.

  ![Select a group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-assignment-azure-portal/select-a-group.png)

6. On the **Assign license** blade, click **Assignment options (optional)**, which displays all service plans included in the two products that we selected previously. Find **Yammer Enterprise** and turn it **Off** to disable that service from the product license. Confirm by clicking **OK** at the bottom of **Assignment options**.

  ![Assignment options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-assignment-azure-portal/assignment-options.png)

7. Finally, on the **Assign license** blade, click **Assign** at the bottom of the blade to complete the assignment.

8. A notification is displayed in the upper right corner that shows the status and outcome of the process. If the assignment to the group couldn't be completed (for example, because of pre-existing licenses in the group), click the notification to view details of the failure.

We've now specified a license template for the HR Department group. A background process in Azure AD has been started to process all existing members of that group. This initial operation might take some time, depending on the current size of the group. In the next step, we'll describe how to verify that the process has completed and if further attention is required to resolve problems.

> [!NOTE]
> You can start the same assignment from an alternative location: **Users and groups** in Azure AD. Go to **Azure Active Directory** > **Users and groups** > **All groups**. Then find the group, select it, and go to the **Licenses** tab. The **Assign** button on top of the blade will open the license assignment blade.

## <a name="step-2-verify-that-the-initial-assignment-has-completed"></a>Step 2: Verify that the initial assignment has completed

1. Go to **Azure Active Directory** > **Users and groups** > **All groups**. Then find the *HR Department* group that licenses were assigned to.

2. On the *HR Department* group blade, select **Licenses** to quickly confirm if licenses have been fully assigned to users, and if there are any errors that you need to look into. The following information is available:

  - List of product licenses that are currently assigned to the group. Select an entry to show the specific services that have been enabled and to make changes.

  - Status of the latest license changes that were made to the group (if the changes are being processed or if processing has finished for all user members).

  - Information about users that are in an error state because licenses couldn't be assigned to them.

  ![Assignment options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-assignment-azure-portal/assignment-errors.png)

3. See more detailed information about license processing under **Azure Active Directory** > **Users and groups** > *group name* > **Audit logs**. Note the following activities:

  - Activity: **Start applying group based license to users**. This is logged when the system picks up the license assignment change on the group and starts applying it to all user members. It contains information about the change that was made.

  - Activity: **Finish applying group based license to users**. This is logged when the system finishes processing all users in the group. It contains a summary of how many users were successfully processed and how many users couldn't be assigned group licenses.

## <a name="step-3-check-for-license-problems-and-resolve-them"></a>Step 3: Check for license problems and resolve them

1. Go to **Azure Active Directory** > **Users and groups** > **All groups**, and find the *HR Department* group that licenses were assigned to.
2. On the **HR Department** group blade, select **Licenses**. The notification on top of the blade shows that there are 10 users that licenses couldn't be assigned to. Clicking it opens a list of all users in a licensing error state for this group.
3. The **Failed assignments** column tells us that both product licenses couldn't be assigned to the users. **Top reason for failure** contains the cause of the failure. In this case, it's **Conflicting service plans**.

  ![Failed assignments](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-assignment-azure-portal/failed-assignments.png)

4. Select a user to open the **Licenses** blade. This blade shows all licenses that are currently assigned to the user. In this example, we can see the user has the Office 365 Enterprise E1 license that was inherited from the **Kiosk users** group. This conflicts with the E3 license that the system tried to apply from the **HR Department** group. As a result, none of the licenses from that group have been assigned to the user.

  ![View licenses for a user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-assignment-azure-portal/user-license-view.png)

5. To solve this, we remove the user from the **Kiosk users** group. After Azure AD processes the change, the **HR Department** licenses are correctly assigned.

  ![License correctly assigned](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-assignment-azure-portal/license-correctly-assigned.png)

## <a name="next-steps"></a>Next steps

To learn more about the feature set for license management through groups, see the following:

* [What is group-based licensing in Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Identifying and resolving license problems for a group in Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [How to migrate individual licensed users to group-based licensing in Azure Active Directory](active-directory-licensing-group-migration-azure-portal.md)
* [Azure Active Directory group-based licensing additional scenarios](active-directory-licensing-group-advanced.md)







