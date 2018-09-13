---
title: Configure Azure AD directory role settings in PIM | Microsoft Docs
description: Learn how to configure Azure AD directory role settings in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: pim
ms.date: 08/27/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 2d7226f18eb922eaba3c8184656560c33202ef56
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868251"
---
# <a name="configure-azure-ad-directory-role-settings-in-pim"></a>Configure Azure AD directory role settings in PIM

A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.

## <a name="open-role-settings"></a>Open role settings

Follow these steps to open the settings for an Azure AD directory role.

1. Open **Azure AD Privileged Identity Management**.

1. Click **Azure AD directory roles**.

1. Click **Settings**.

    ![Azure AD directory roles - Settings](./media/pim-how-to-change-default-settings/pim-directory-roles-settings.png)

1. Click **Roles**.

1. Click the role whose settings you want to configure.

    ![Azure AD directory roles - Settings Roles](./media/pim-how-to-change-default-settings/pim-directory-roles-settings-role.png)

    On the settings page for each role, there are several settings you can configure. These settings only affect users who are **eligible** assignments, not **permanent** assignments.

## <a name="activations"></a>Activations

Use the **Activations** slider to set the maximum time, in hours, that a role stays active before it expires. This value can be between 1 and 72 hours.

## <a name="notifications"></a>Notifications

Use the **Notifications** switch to specify whether the system sends emails to administrators confirming that they have activated a role. This can be useful for detecting unauthorized or illegitimate activations.

## <a name="incidentrequest-ticket"></a>Incident/Request ticket

Use the **Incident/Request ticket** switch to specify whether to require eligible administrators to include a ticket number when they activate their role. This can be useful when you perform role access audits.

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication

Use the **Multi-Factor Authentication** switch to specify whether to require users to verify their identity with MFA before they can activate their roles. They only have to verify this once per session, not every time they activate a role. There are two tips to keep in mind when you enable MFA:

* Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA. If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.
* You cannot disable MFA for highly privileged roles for Azure AD and Office365. This is a safety feature because these roles should be carefully protected:  
  
  * Application administrator
  * Application Proxy server administrator
  * Billing administrator  
  * Compliance administrator  
  * CRM service administrator
  * Customer LockBox access approver
  * Directory writer  
  * Exchange administrator  
  * Global administrator
  * Intune service administrator
  * Mailbox administrator  
  * Partner tier1 support  
  * Partner tier2 support  
  * Privileged role administrator
  * Security administrator  
  * SharePoint administrator  
  * Skype for Business administrator  
  * User account administrator  

For more information, see [Multi-factor authentication (MFA) and PIM](pim-how-to-require-mfa.md).

## <a name="require-approval"></a>Require approval

If you want to require approval to activate a role, follow these steps.

1. Set the **Require approval** switch to **Enabled**. The pane expands with options to select approvers.

    ![Azure AD directory roles - Settings - Require approval](./media/pim-how-to-change-default-settings/pim-directory-roles-settings-require-approval.png)

    If you **DO NOT** specify any approvers, the Privileged Role Administrators become the default approvers. Privileged Role Administrators would be required to approve **ALL** activation requests for this role.

1. To specify approvers, click **Select approvers**.

    ![Azure AD directory roles - Settings - Require approval](./media/pim-how-to-change-default-settings/pim-directory-roles-settings-require-approval-select-approvers.png)

1. Select one or more approvers and then click **Select**. You can select users or groups. At least 2 approvers is recommended. Self-approval is not allowed.

    Your selections will appear in the list of selected approvers.

1. Once you have specified your all your role settings, click **Save** to save your changes.


<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

## <a name="next-steps"></a>Next steps

- [Assign Azure AD directory roles in PIM](pim-how-to-add-role-to-user.md)
- [Configure security alerts for Azure AD directory roles in PIM](pim-how-to-configure-security-alerts.md)
