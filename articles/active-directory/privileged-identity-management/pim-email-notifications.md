---
title: Email notifications in PIM - Azure | Microsoft Docs
description: Describes email notifications in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: pim
ms.date: 09/07/2018
ms.author: rolyon
ms.reviewer: hanki
ms.custom: pim
ms.openlocfilehash: de1d29d3ab1b370257c3a2d6b6ff9f677197fc2a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865367"
---
# <a name="email-notifications-in-pim"></a>Email notifications in PIM

When key events occur in Azure AD Privileged Identity Management (PIM), email notifications are sent. For example, PIM sends emails for the following events:

- When a privileged role activation is pending approval
- When a privileged role activation request is completed
- When a privileged role is activated
- When a privileged role is assigned
- When Azure AD PIM is enabled

Email notifications are sent to the following administrators:

- Privileged Role Administrator
- Security Administrator

Email notifications are also sent to the end user who has the privileged role for the following events:

- When a privileged role activation request is completed
- When a privileged role is assigned

Starting at the end of July 2018, email notifications sent through PIM have a new sender email address and a new visual design. This update will impact both PIM for Azure AD and PIM for Azure resources. All events that previously triggered an email notification will continue to send out an email. Some emails will have updated content providing more targeted information.

## <a name="sender-email-address"></a>Sender email address

Starting at the end of July 2018, email notifications have the following address:

- Email address:  **azure-noreply@microsoft.com**
- Display name: Microsoft Azure

Previously, email notifications had the following address:

- Email address:  **azureadnotifications@microsoft.com**
- Display name: Microsoft Azure AD Notification Service

## <a name="email-subject-line"></a>Email subject line

Starting at the end of July 2018, email notifications for both Azure AD and Azure resource roles will have a **PIM** prefix in the subject line. Here's an example:

- PIM: Alain Charon was permanently assigned the Backup Reader role.

## <a name="pim-emails-for-azure-ad-roles"></a>PIM emails for Azure AD roles

Starting at the end of July 2018, the PIM email notifications for Azure AD roles have an updated design. The following shows an example email that is sent when a user activates a privileged role for the fictional Contoso organization.

![New PIM email for Azure AD roles](./media/pim-email-notifications/email-directory-new.png)

Previously, when a user activated a privileged role, the email looked like the following.

![Old PIM email for Azure AD roles](./media/pim-email-notifications/email-directory-old.png)

## <a name="pim-emails-for-azure-resource-roles"></a>PIM emails for Azure resource roles

Starting at the end of July 2018, the PIM email notifications for Azure resource roles have an updated design. The following shows an example email that is sent when a user is assigned a privileged role for the fictional Contoso organization.

![New PIM email for Azure resource roles](./media/pim-email-notifications/email-resources-new.png)

Previously, when a user was assigned a privileged role, the email looked like the following.

![Old PIM email for Azure resource roles](./media/pim-email-notifications/email-resources-old.png)

## <a name="next-steps"></a>Next steps

- [Configure Azure AD directory role settings in PIM](pim-how-to-change-default-settings.md)
- [Approve or deny requests for Azure AD directory roles in PIM](azure-ad-pim-approval-workflow.md)
