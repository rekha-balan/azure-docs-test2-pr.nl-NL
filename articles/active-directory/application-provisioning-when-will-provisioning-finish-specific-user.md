---
title: Find out when a specific user will be able to access an application | Microsoft Docs
description: How to find out when a critically important user be able to access an application you have configured for user provisioning with Azure AD
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
ms.openlocfilehash: fe99a817f69465238ab71e71e049375fd8547a1f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564328"
---
# <a name="find-out-when-a-specific-user-will-be-able-to-access-an-application"></a>Find out when a specific user will be able to access an application
When using automatic user provisioning with an application, Azure AD automatically provision and update user accounts in an app based on things like [user and group assignment](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) at a regularly scheduled time interval, typically every 10 minutes.

## <a name="how-long-does-it-take"></a>How long does it take?

The time it takes for a given user to be provisioned depends mainly on whether or not an initial “full” sync has already occurred.

The first sync between Azure AD and an app can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning. 

Subsequent syncs after the initial sync be faster (e.g. within 10 minutes), as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.

## <a name="how-to-check-the-status-of-a-user"></a>How to check the status of a user

To see the provisioning status for a selected user, consult the Audit logs in Azure AD.

The provisioning audit logs can be accessed in the Azure portal, in the **Azure Active Directory &gt; Enterprise Apps &gt; \[Application Name\] &gt; Audit Logs** tab. Filter the logs on the **Account Provisioning** category to only see the provisioning events for that app. You can search for users based on the “matching ID” that was configured for them in the attribute mappings. 

For example, if you configured the “user principal name” or “email address” as the matching attribute on the Azure AD side, and the user not being provisioning has a value of “audrey@contoso.com”, then search the audit logs for “audrey@contoso.com” and review then entries returned.

The provisioning audit logs record all the operations performed by the provisioning service, including:

* Querying Azure AD for assigned users that are in scope for provisioning
* Querying the target app for the existence of those users
* Comparing the user objects between the system
* Adding, updating, or disabling the user account in the target system based on the comparison

## <a name="next-steps"></a>Next steps
[Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''
