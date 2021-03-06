---
title: Azure Active Directory Identity Protection notifications| Microsoft Docs
description: Learn how notifications support your investigation activities.
services: active-directory
keywords: azure active directory identity protection, cloud app discovery, managing applications, security, risk, risk level, vulnerability, security policy
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/09/2017
ms.author: markvi
ms.openlocfilehash: e1c99798f58a7d434116103b30652a098edd7aa8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553815"
---
# <a name="azure-active-directory-identity-protection-notifications"></a>Azure Active Directory Identity Protection notifications
Azure AD Identity Protection sends two types of automated notification emails to help you manage user risk and risk events:

* User compromised alert email
* Weekly digest email

## <a name="user-compromised-alert-email"></a>User compromised alert email
A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised. The email includes a link to the Users flagged for risk report in the Identity Protection dashboard. We recommend that you immediately investigate notifications of compromised accounts.

## <a name="weekly-digest-email"></a>Weekly digest email
The weekly digest email contains a summary of new risk events.<br>
It includes:

* Users at risk
* Suspicious activities
* Detected vulnerabilities
* Links to the related reports in Identity Protection

<br>
![Remediation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-notifications/400.png "Remediation")
<br>

You can switch sending a weekly digest email off.
<br><br>
![User risks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-notifications/62.png "User risks")
<br>

**To open the related configuration dialog**:

1. On the **Azure AD Identity Protection** blade, click **Settings**.
   <br><br>
   ![User risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-notifications/401.png "User risk policy")
   <br>
2. In the **General** section, click **Notifications**.
   <br><br>
   ![User risk policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-notifications/405.png "User risk policy")
   <br>

## <a name="see-also"></a>See also
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)




