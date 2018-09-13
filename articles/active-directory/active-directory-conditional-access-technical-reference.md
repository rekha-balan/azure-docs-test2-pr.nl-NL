---
title: Azure Active Directory Conditional Access technical reference | Microsoft Docs
description: With Conditional access control, Azure Active Directory checks the specific conditions you pick when authenticating the user and before allowing access to the application. Once those conditions are met, the user is authenticated and allowed access to the application.
services: active-directory.
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 56a5bade-7dcc-4dcf-8092-a7d4bf5df3c1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/28/2017
ms.author: markvi
ms.openlocfilehash: 734491c1cd929de27dc166692f6893b2c2f2fdfe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551209"
---
# <a name="azure-active-directory-conditional-access-technical-reference"></a>Azure Active Directory Conditional Access technical reference

## <a name="services-enabled-with-conditional-access"></a>Services enabled with conditional access

Conditional Access rules are supported across various Azure AD application types. This list includes:


* Applications registered with the Azure Application Proxy
* Azure Remote App
* Developed line of business and multi-tenant applications registered with Azure AD
* Dynamics CRM
* Federated applications from the Azure AD application gallery
* Microsoft Office 365 Yammer
* Microsoft Office 365 Exchange Online
* Microsoft Office 365 SharePoint Online (includes OneDrive for Business)
* Microsoft Power BI 
* Password SSO applications from the Azure AD application gallery
* Visual Studio Online









## <a name="enable-access-rules"></a>Enable access rules
Each rule can be enabled or disabled on a per application bases. When rules are **ON** they will be enabled and enforced for users accessing the application. When they are **OFF** they will not be used and will not impact the users sign in experience.

## <a name="applying-rules-to-specific-users"></a>Applying rules to specific users
Rules can be applied to specific sets of users based on security group by setting **Apply To**. **Apply To** can be set to **All Users** or **Groups**. When set to **All Users** the rules will apply to any user with access to the application. The **Groups** option allows specific security and distribution groups to be selected, rules will only be enforced for these groups.

When deploying a rule,  it is common to first apply it a limited set of users, that are members of a piloting groups. Once complete the rule can be applied to **All Users**. This will cause the rule to be enforced for all users in the organization.

Select groups may also be exempted from policy using the **Except** option. Any members of these groups will be exempted even if they appear in an included group.

## <a name="at-work-networks"></a>“At work” networks
Conditional access rules that use an “At work” network, rely on trusted IP address ranges that have been configured in Azure AD, or use of the "inside corpnet" claim from AD FS. These rules include:

* Require multi-factor authentication when not at work
* Block access when not at work

Options for specifiying “at work” networks

1. Configure trusted IP address ranges in the [multi-factor authentication configuration page](../multi-factor-authentication/multi-factor-authentication-whats-next.md). Conditional Access policy will use the configured ranges on each authentication request and token issuance to evaluate rules. 
2. Configure use of the inside corpnet claim, this option can be used with federated directories, using AD FS. To learn more about the inside corpnet claims, see [Tusted IPs](../multi-factor-authentication/multi-factor-authentication-whats-next.md#trusted-ips).


## <a name="rules-based-on-application-sensitivity"></a>Rules based on application sensitivity
Rules are configured per application allowing the high value services to be secured without impacting access to other services. Conditional access rules can be configured on the  **Configure** tab of the application. 

Rules currently offered:

* **Require multi-factor authentication**
  
  * All users that this policy is applied to will be required to authenticate via multi-factor authentication at least once.
* **Require multi-factor authentication when not at work**
  
  * If this policy is applied, all users will be required to have performed multi-factor authentication at least once if they access the service from a non-work remote location. If they move from a work to remote location, they will be required to perform multifactor authentication when accessing the service.
* **Block access when not at work** 
  
  * When users move from work to a remote location, they will be blocked if the "Block access when not at work" policy is applied to them.  They will be re-allowed access when at a work location.

## <a name="related-topics"></a>Related topics
* [Securing access to Office 365 and other apps connected to Azure Active Directory](active-directory-conditional-access.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)

