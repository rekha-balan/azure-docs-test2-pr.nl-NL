---
title: How to configure security alerts | Microsoft Docs
description: Learn how to configure security alerts for Azure Privileged Identity Management extension.
services: active-directory
documentationcenter: ''
author: billmath
manager: femila
editor: ''
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: 5998517cf53fcc5c9b23cd8b45a0e7d71b1d1fff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661866"
---
# <a name="how-to-configure-security-alerts-in-azure-ad-privileged-identity-management"></a>How to configure security alerts in Azure AD Privileged Identity Management
## <a name="security-alerts"></a>Security alerts
Azure Privileged Identity Management (PIM) generates alerts when there is suspicious or unsafe activity in your environment. When an alert is triggered, it shows up on the PIM dashboard. Select the alert to see a report that lists the users or roles that triggered the alert.

![PIM dashboard security alerts - screenshot][1]

| Alert | Trigger | Recommendation |
| --- | --- | --- |
| **Roles are being assigned outside of PIM** |An administrator was permanently assigned to a role, outside of the PIM interface. |Review the new role assignment. Since other services can only assign permanent administrators, change it to an eligible assignment if necessary. |
| **Roles are being activated too frequently** |There were too many reactivations of the same role within the time allowed in the settings. |Contact the user to see why they have activated the role so many times. Maybe the time limit is too short for them to complete their tasks, or maybe they're using scripts to automatically activate a role. |
| **Roles don't require multi-factor authentication for activation** |There are roles without MFA enabled in the settings. |We require MFA for the most highly privileged roles, but strongly encourage that you enable MFA for activation of all roles. |
| **Administrators aren't using their privileged roles** |There are eligible administrators that haven’t activated their roles recently. |Start an access review to determine the users that don't need access anymore. |
| **There are too many global administrators** |There are more global administrators than recommended. |If you have a high number of global administrators, it's likely that users are getting more permissions than they need. Move users to less privileged roles, or make some of them eligible for the role instead of permanently assigned. |

## <a name="configure-security-alert-settings"></a>Configure security alert settings
You can customize some of the security alerts in PIM to work with your environment and security goals. Follow these steps to reach the settings blade:

1. Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** tile from the dashboard.
2. Select **Managed privileged roles** > **Settings** > **Alerts settings**.
   
    ![Navigate to security alerts settings][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a>"Roles are being activated too frequently" alert
This alert triggers if a user activates the same privileged role multiple times within a specified period. You can configure both the time period and the number of activations.

* **Activation renewal timeframe**: Specify in days, hours, minutes, and second the time period you want to use to track suspicious renewals.
* **Number of activation renewals**: Specify the number of activations, from 2 to 100, that you consider worthy of alert, within the timeframe you chose. You can change this setting by moving the slider, or typing a number in the text box.

### <a name="there-are-too-many-global-administrators-alert"></a>"There are too many global administrators" alert
PIM triggers this alert if two different criteria are met, and you can configure both of them. First, you need to reach a certain threshold of global administrators. Second, a certain percentage of your total role assignments must be global administrators. If you only meet one of these measurements, the alert does not appear.  

* **Minimum number of Global Administrators**: Specify the number of global administrators, from 2 to 100, that you consider an unsafe amount.
* **Percentage of global administrators**: Specify the percentage of administrators who are global administrators, from 0% to 100%, that is unsafe in your environment.

### <a name="administrators-arent-using-their-privileged-roles-alert"></a>"Administrators aren't using their privileged roles" alert
This alert triggers if a user goes a certain amount of time without activating a role.

* **Number of days**: Specify the number of days, from 0 to 100, that a user can go without activating a role.

## <a name="next-steps"></a>Next steps
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png


