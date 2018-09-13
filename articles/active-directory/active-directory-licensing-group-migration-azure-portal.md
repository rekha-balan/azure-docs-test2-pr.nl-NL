---
title: How to migrate your individual licensed users to a group  in Azure Active Directory | Microsoft Docs
description: How to switch from individual user licenses to group-based licensing using Azure Active Directory
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
ms.date: 02/28/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 431f72e45732aaf11dab1dc1686e4a2b3940946f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660551"
---
# <a name="how-to-add-licensed-users-to-a-group-for-licensing-in-azure-active-directory"></a>How to add licensed users to a group for licensing in Azure Active Directory

You may have existing licenses deployed to users in the organizations via “direct assignment”; that is, using PowerShell scripts or other tools to assign individual user licenses. If you would like to start using group-based licensing to manage licenses in your organization, you will need a migration plan to seamlessly replace existing solutions with group-based licensing.

The most important thing to keep in mind is that you should avoid a situation where migrating to group-based licensing will result in users temporarily losing their currently assigned licenses. Any process that may result in removal of licenses should be avoided to remove the risk of users losing access to services and their data.

## <a name="recommended-migration-process"></a>Recommended migration process

1. You have existing automation (for example, PowerShell) managing license assignment and removal for users. Leave it running as is.

2. Create a new licensing group (or decide which existing groups to use) and make sure that all required users are added as members.

3. Assign the required licenses to those groups; your goal should be to reflect the same licensing state your existing automation (for example, PowerShell) is applying to those users.

4. Verify that licenses have been applied to all users in those groups. This can be done by checking the processing state on each group and by checking Audit Logs.

  - You can spot check individual users by looking at their license details. You will see that they have the same licenses assigned “directly” and “inherited” from groups.

  - You can run a PowerShell script to [verify how licenses are assigned to users](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).

  - When the same product license is assigned to the user both directly and through a group, only one license is consumed by the user. Hence no additional licenses are required to perform migration.

5. Verify that no license assignments failed by checking each group for users in error state. For more information, see [Identifying and resolving license problems for a group](active-directory-licensing-group-problem-resolution-azure-portal.md).

6. Consider removing the original direct assignments; you may want to do it gradually, in “waves”, to monitor the outcome on a subset of users first.

  You could leave the original direct assignments on users, but when the users leave their licensed groups they will still retain the original license, which is possibly not want you want.

## <a name="an-example"></a>An example

We have an organization with 1,000 users. All users require Enterprise Mobility + Security (EMS) licenses. 200 users are in the Finance Department and require Office 365 Enterprise E3 licenses. We have a PowerShell script running on premises adding and removing licenses from users as they come and go. We want to replace the script with group-based licensing so licenses are managed automatically by Azure AD.

Here is what the migration process could look like:

1. Using the Azure portal assign the EMS license to the **All users** group in Azure AD. Assign the E3 license to the **Finance department** group that contains all the required users.

2. For each group, confirm that license assignment has completed for all users. Go to the blade for each group, select **Licenses**, and check the processing status at the top of the **Licenses** blade.

  - Look for “Latest license changes have been applied to all users" to confirm processing has completed.

  - Look for a notification on top about any users for whom licenses may have not been successfully assigned. Did we run out of licenses for some users? Do some users have conflicting license SKUs that prevent them from inheriting group licenses?

3. Spot check some users to verify that they have both the direct and group licenses applied. Go to the blade for a user, select **Licenses**, and examine the state of licenses.

  - This is the expected user state during migration:

      ![expected user state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  This confirms that the user has both direct and inherited licenses. We see that both **EMS** and **E3** are assigned.

  - Select each license to show details about the enabled services. This can be used to check if the direct and group licenses enable exactly the same service plans for the user.

      ![check service plans](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. After confirming that both direct and group licenses are equivalent, you can start removing direct licenses from users. You can test this by removing them for individual users in the portal and then run automation scripts to have them removed in bulk. Here is an example of the same user with the direct licenses removed through the portal. Notice that the license state remains unchanged, but we no longer see direct assignments.

  ![direct licenses removed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a>Next steps

To learn more about other scenarios for license management through groups, read

* [Assigning licenses to a group in Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md)
* [What is group-based licensing in Azure Active Directory?](active-directory-licensing-whatis-azure-portal.md)
* [Identifying and resolving license problems for a group in Azure Active Directory](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [Azure Active Directory group-based licensing additional scenarios](active-directory-licensing-group-advanced.md)



