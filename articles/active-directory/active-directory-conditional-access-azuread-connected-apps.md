---
title: Azure Conditional Access for SaaS Apps| Microsoft Docs
description: 'Conditional access in Azure AD allows you to configure per-application multi-factor authentication access rules and the ability to block access for users not on a trusted network. '
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: markvi
ms.openlocfilehash: dc1c13e312cff0923f41af17dbbe7a104a9b7fa7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551975"
---
# <a name="getting-started-with-azure-active-directory-conditional-access"></a>Getting started with Azure Active Directory Conditional Access
Azure Active Directory Conditional Access for [SaaS](https://azure.microsoft.com/overview/what-is-saas/) apps and Azure AD connected apps lets you configure conditional access based on group, location, and application sensitivity. 

With conditional access based on application sensitivity, you can set multi-factor authentication (MFA) access rules per application. MFA per application provides the ability to block access for users who are not on a trusted network. You can apply MFA rules to all users that are assigned to the application, or only for users within specified security groups.  Users may be excluded from the MFA requirement if they are accessing the application from an IP address that is inside the organization’s network.

These capabilities will be available to customers that have purchased an Azure Active Directory Premium license.

## <a name="scenario-prerequisites"></a>Scenario prerequisites
* License for Azure Active Directory Premium
* Federated or managed Azure Active Directory tenant
* Federated tenants require that multi-factor authentication be enabled.

## <a name="configure-per-application-access-rules"></a>Configure per-application access rules
This section describes how to configure per-application access rules.

1. Sign in to the Azure classic portal Using an account that is a global administrator for Azure AD.
2. On the left pane, select **Active Directory**.
3. On the Directory tab, select your directory.
4. Select the **Applications** tab.
5. Select the application that the rule will be set for.
6. Select the **Configure** tab.
7. Scroll down to the access rules section. Select the desired access rule.
8. Specify the users the rule will apply to.
9. Enable the policy by selecting **Enabled to be On**.

## <a name="understanding-access-rules"></a>Understanding access rules
This section gives a detailed description of the access rules supported in the Azure Conditional Application Access.

### <a name="specifying-the-users-the-access-rules-apply-to"></a>Specifying the users the access rules apply to
By default the policy will apply to all users that have access to the application. However, you can also restrict the policy to users that are members of the specified security groups. The **Add Group** button is used to select one or more groups from the group selection dialog that the access rule will apply to. This dialog can also be used to remove selected groups. When the rules are selected to apply to Groups, the access rules will only be enforced for users that belong to one of the specified security groups.

Security groups can also be explicitly excluded from the policy by selecting the **Except** option and specifying one or more groups. Users that are a member of a group in the **Except** list will not be subject to the multi-factor authentication requirement, even if they are a member of a group that the access rule applies to.
The access rule shown below will require all users in the Managers group to use multi-factor authentication when accessing the application.

![Setting conditional access rules with MFA](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-azuread-connected-apps/conditionalaccess-saas-apps.png)

## <a name="conditional-access-rules-with-mfa"></a>Conditional Access Rules with MFA
If a user has been configured using the per-user multi-factor authentication feature, this setting on the user will combine with the multi-factor authentication rules of the app. This means a user that has been configured for per-user multi-factor authentication will be required to perform multi-factor authentication even if they have been exempted from the application multi-factor authentication rules. Learn more about multi-factor authentication and per-user settings.

### <a name="access-rule-options"></a>Access rule options
The following options are supported:

* **Require multi-factor authentication**: The users to whom the access rules apply to, will be required to complete multi-factor authentication before accessing the application that the policy applies to.
* **Require multi-factor authentication when not at work**: A user that is coming from a trusted IP address will not be required to perform multi-factor authentication. The trusted IP address ranges can be configured on the multi-factor authentication settings page.
* **Block access when not at work**: A user that is not coming from a trusted IP address will be blocked. The trusted IP address ranges can be configured on the multi-factor authentication settings page.

### <a name="setting-rule-status"></a>Setting rule status
Access rule status allows turning the rules on or off. When the access rules are off, the multi-factor authentication requirement is not enforced.

### <a name="access-rule-evaluation"></a>Access rule evaluation
Access rules are evaluated when a user accesses a federated application that uses OAuth 2.0, OpenID Connect, SAML or WS-Federation. In addition, access rules are evaluated when the OAuth 2.0 and OpenID Connect use a refresh token to acquire an access token. If policy evaluation fails when a refresh token is used, the error **invalid_grant** will be returned, this indicates the user needs to re-authenticate to the client.

### <a name="configure-federation-services-to-provide-multi-factor-authentication"></a>Configure federation services to provide multi-factor authentication
For federated tenants, MFA may be performed by Azure Active Directory or by the on-premises AD FS server.

By default, MFA will occur at a page hosted by Azure Active Directory. To configure MFA on-premises, the **–SupportsMFA** property must be set to **true** in Azure Active Directory, by using the Azure AD module for Windows PowerShell.

The following example shows how to enable on-premises MFA by using the [Set-MsolDomainFederationSettings cmdlet](https://msdn.microsoft.com/library/azure/dn194088.aspx) on the contoso.com tenant:

    Set-MsolDomainFederationSettings -DomainName contoso.com -SupportsMFA $true

In addition to setting this flag, the federated tenant AD FS instance must be configured to perform multi-factor authentication. Follow the instructions for [deploying Azure Multi-Factor Authentication on-premises](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="related-articles"></a>Related Articles
* [Securing access to Office 365 and other apps connected to Azure Active Directory](active-directory-conditional-access.md)
* [Article Index for Application Management in Azure Active Directory](active-directory-apps-index.md)


