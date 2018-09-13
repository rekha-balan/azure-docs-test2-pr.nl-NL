---
title: Configure security alerts for Azure resource roles in PIM | Microsoft Docs
description: Learn how to configure security alerts for Azure resource roles in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: pim
ms.date: 04/02/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 2fa63cf2fa05f2cde4558f0bea38bfd7f17df3ae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968794"
---
# <a name="configure-security-alerts-for-azure-resource-roles-in-pim"></a>Configure security alerts for Azure resource roles in PIM
Privileged Identity Management (PIM) for Azure Resources generates alerts when there is suspicious or unsafe activity in your environment. When an alert is triggered, it shows up on the Alerts page. 

![Alerts page](media/azure-pim-resource-rbac/RBAC-alerts-home.png)

## <a name="review-alerts"></a>Review alerts
Select an alert to see a report that lists the users or roles that triggered the alert, along with remediation advice.

![Alert report](media/azure-pim-resource-rbac/rbac-alert-info.png)

## <a name="alerts"></a>Alerts
| Alert | Severity | Trigger | Recommendation |
| --- | --- | --- | --- |
| **Too many owners assigned to a resource** |Medium |Too many users have the owner role. |Review the users in the list and reassign some to less privileged roles. |
| **Too many permanent owners assigned to a resource** |Medium |Too many users are permanently assigned to a role. |Review the users in the list and re-assign some to require activation for role use. |
| **Duplicate role created** |Medium |Multiple roles have the same criteria. |Use only one of these roles. |


### <a name="severity"></a>Severity
* **High**: Requires immediate action because of a policy violation. 
* **Medium**: Does not require immediate action but signals a potential policy violation.
* **Low**: Does not require immediate action but suggests a preferred policy change.

## <a name="configure-security-alert-settings"></a>Configure security alert settings
From the Alerts page, go to **Settings**.
![Settings](media/azure-pim-resource-rbac/rbac-navigate-settings.png)

Customize settings on the different alerts to work with your environment and security goals.
![Customize settings](media/azure-pim-resource-rbac/rbac-alert-settings.png)

## <a name="next-steps"></a>Next steps

- [Configure security alerts for Azure resource roles in PIM](pim-resource-roles-configure-alerts.md)
