---
title: 'Azure Active Directory Domain Services: Synchronization in managed domains | Microsoft Docs'
description: Understand synchronization in an Azure Active Directory Domain Services managed domain
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 57cbf436-fc1d-4bab-b991-7d25b6e987ef
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4a008e5e7351f55fc7db659e9090777f8d66f310
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555092"
---
# <a name="synchronization-in-an-azure-ad-domain-services-managed-domain"></a>Synchronization in an Azure AD Domain Services managed domain
The following diagram illustrates how synchronization works in Azure AD Domain Services managed domains.

![Synchronization topology in Azure AD Domain Services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-design-guide/sync-topology.png)

## <a name="synchronization-from-your-on-premises-directory-to-your-azure-ad-tenant"></a>Synchronization from your on-premises directory to your Azure AD tenant
Azure AD Connect sync is used to synchronize user accounts, group memberships, and credential hashes to your Azure AD tenant. Attributes of user accounts such as the UPN and on-premises SID (security identifier) are synchronized. If you use Azure AD Domain Services, legacy credential hashes required for NTLM and Kerberos authentication are also synchronized to your Azure AD tenant.

If you configure write-back, changes occurring in your Azure AD directory are synchronized back to your on-premises Active Directory. For example, if you change your password using Azure AD's self-service password change features, the changed password is updated in your on-premises AD domain.

> [!NOTE]
> Always use the latest version of Azure AD Connect to ensure you have fixes for all known bugs.
>
>

## <a name="synchronization-from-your-azure-ad-tenant-to-your-managed-domain"></a>Synchronization from your Azure AD tenant to your managed domain
User accounts, group memberships, and credential hashes are synchronized from your Azure AD tenant to your Azure AD Domain Services managed domain. This synchronization process is automatic. You do not need to configure, monitor, or manage this synchronization process. After the one-time initial synchronization of your directory is complete, it typically takes about 20 minutes for changes made in Azure AD to be reflected in your managed domain. This synchronization interval applies to password changes or changes to attributes made in Azure AD.

The synchronization process is also one-way/unidirectional in nature. Your managed domain is largely read-only except for any custom OUs you create. Therefore, you cannot make changes to user attributes, user passwords, or group memberships within the managed domain. As a result, there is no reverse synchronization of changes from your managed domain back to your Azure AD tenant.

## <a name="synchronization-from-a-multi-forest-on-premises-environment"></a>Synchronization from a multi-forest on-premises environment
Many organizations have a fairly complex on-premises identity infrastructure consisting of multiple account forests. Azure AD Connect supports synchronizing users, groups, and credential hashes from multi-forest environments to your Azure AD tenant.

In contrast, your Azure AD tenant is a much simpler and flat namespace. To enable users to reliably access applications secured by Azure AD, resolve UPN conflicts across user accounts in different forests. Your Azure AD Domain Services managed domain bears close resemblance to your Azure AD tenant. Therefore, you see a flat OU structure in your managed domain. All users and groups are stored within the 'AADDC Users' container, regardless of the on-premises domain or forest from which they were synced in. You may have configured a hierarchical OU structure on-premises. However, your managed domain still has a simple flat OU structure.

## <a name="exclusions---what-isnt-synchronized-to-your-managed-domain"></a>Exclusions - what isn't synchronized to your managed domain
The following objects or attributes are not synchronized to your Azure AD tenant or to your managed domain:

* **Excluded attributes:** You may choose to exclude certain attributes from synchronizing to your Azure AD tenant from your on-premises domain using Azure AD Connect. These excluded attributes are not available in your managed domain.
* **Group Policies:** Group Policies configured in your on-premises domain are not synchronized to your managed domain.
* **SYSVOL share:** Similarly, the contents of the SYSVOL share on your on-premises domain are not synchronized to your managed domain.
* **Computer objects:** Computer objects for computers joined to your on-premises domain are not synchronized to your managed domain. These computers do not have a trust relationship with your managed domain and belong to your on-premises domain only. In your managed domain, you find computer objects only for computers you have explicitly domain-joined to the managed domain.
* **SidHistory attributes for users and groups:** The primary user and primary group SIDs from your on-premises domain are synchronized to your managed domain. However, existing SidHistory attributes for users and groups are not synchronized from your on-premises domain to your managed domain.
* **Organization Units (OU) structures:** Organizational Units defined in your on-premises domain do not synchronize to your managed domain. There are two built-in OUs in your managed domain. By default, your managed domain has a flat OU structure. You may however choose to [create a custom OU in your managed domain](active-directory-ds-admin-guide-create-ou.md).

## <a name="how-specific-attributes-are-synchronized-to-your-managed-domain"></a>How specific attributes are synchronized to your managed domain
The following table lists some common attributes and describes how they are synchronized to your managed domain.

| Attribute in your managed domain | Source | Notes |
|:--- |:--- |:--- |
| UPN |User's UPN attribute in your Azure AD tenant |The UPN attribute from your Azure AD tenant is synchronized as is to your managed domain. Therefore, the most reliable way to sign in to your managed domain is using your UPN. |
| SAMAccountName |User's mailNickname attribute in your Azure AD tenant or auto-generated |The SAMAccountName attribute is sourced from the mailNickname attribute in your Azure AD tenant. If multiple user accounts have the same mailNickname attribute, the SAMAccountName is auto-generated. If the user's mailNickname or UPN prefix is longer than 20 characters, the SAMAccountName is auto-generated to satisfy the 20 character limit on SAMAccountName attributes. |
| Passwords |User's password from your Azure AD tenant |Credential hashes required for NTLM or Kerberos authentication (also called supplemental credentials) are synchronized from your Azure AD tenant. If your Azure AD tenant is a synced tenant, these credentials are sourced from your on-premises domain. |
| Primary user/group SID |Auto-generated |The primary SID for user/group accounts is auto-generated in your managed domain. This attribute does not match the primary user/group SID of the object in your on-premises AD domain. This mismatch is because the managed domain has a different SID namespace than your on-premises domain. |
| SID history for users and groups |On-premises primary user and group SID |The SidHistory attribute for users and groups in your managed domain is set to match the corresponding primary user or group SID in your on-premises domain. This feature helps make lift-and-shift of on-premises applications to the managed domain easier, since you do not need to re-ACL resources. |

> [!NOTE]
> **Sign in to the managed domain using the UPN format:** The SAMAccountName attribute may be auto-generated for some user accounts in your managed domain. If multiple users have the same mailNickname attribute or users have overly long UPN prefixes, the SAMAccountName for these users may be auto-generated. Therefore, the SAMAccountName format (for example, 'CONTOSO100\joeuser') is not always a reliable way to sign in to the domain. Users' auto-generated SAMAccountName may differ from their UPN prefix. Use the UPN format (for example, 'joeuser@contoso100.com') to sign in to the managed domain reliably.
>
>

### <a name="attribute-mapping-for-user-accounts"></a>Attribute mapping for user accounts
The following table illustrates how specific attributes for user objects in your Azure AD tenant are synchronized to corresponding attributes in your managed domain.

| User attribute in your Azure AD tenant | User attribute in your managed domain |
|:--- |:--- |
| accountEnabled |userAccountControl (sets or clears the ACCOUNT_DISABLED bit) |
| city |l |
| country |co |
| department |department |
| displayName |displayName |
| facsimileTelephoneNumber |facsimileTelephoneNumber |
| givenName |givenName |
| jobTitle |title |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| mailNickname |SAMAccountName (may sometimes be auto-generated) |
| mobile |mobile |
| objectid |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| passwordPolicies |userAccountControl (sets or clears the DONT_EXPIRE_PASSWORD bit) |
| physicalDeliveryOfficeName |physicalDeliveryOfficeName |
| postalCode |postalCode |
| preferredLanguage |preferredLanguage |
| state |st |
| streetAddress |streetAddress |
| surname |sn |
| telephoneNumber |telephoneNumber |
| userPrincipalName |userPrincipalName |

### <a name="attribute-mapping-for-groups"></a>Attribute mapping for groups
The following table illustrates how specific attributes for group objects in your Azure AD tenant are synchronized to corresponding attributes in your managed domain.

| Group attribute in your Azure AD tenant | Group attribute in your managed domain |
|:--- |:--- |
| displayName |displayName |
| displayName |SAMAccountName (may sometimes be auto-generated) |
| mail |mail |
| mailNickname |msDS-AzureADMailNickname |
| objectid |msDS-AzureADObjectId |
| onPremiseSecurityIdentifier |sidHistory |
| securityEnabled |groupType |

## <a name="objects-that-are-not-synchronized-to-your-azure-ad-tenant-from-your-managed-domain"></a>Objects that are not synchronized to your Azure AD tenant from your managed domain
As described in a preceding section of this article, there is no synchronization from your managed domain back to your Azure AD tenant. You may choose to [create a custom Organizational Unit (OU)](active-directory-ds-admin-guide-create-ou.md) in your managed domain. Further, you can create other OUs, users, groups, or service accounts within these custom OUs. None of the objects created within custom OUs are synchronized back to your Azure AD tenant. These objects are available for use only within your managed domain. Therefore, these objects are not visible using Azure AD PowerShell cmdlets, Azure AD Graph API or using the Azure AD management UI.

## <a name="related-content"></a>Related Content
* [Features - Azure AD Domain Services](active-directory-ds-features.md)
* [Deployment scenarios - Azure AD Domain Services](active-directory-ds-scenarios.md)
* [Networking considerations for Azure AD Domain Services](active-directory-ds-networking.md)
* [Get started with Azure AD Domain Services](active-directory-ds-getting-started.md)

