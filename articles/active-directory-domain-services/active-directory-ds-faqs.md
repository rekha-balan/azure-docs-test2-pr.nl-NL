---
title: FAQs - Azure Active Directory Domain Services | Microsoft Docs
description: Frequently asked questions about Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 7f3212350b1158cd51a34ee1b20a456a73d41672
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540793"
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Azure Active Directory Domain Services: Frequently Asked Questions (FAQs)
This page answers frequently asked questions about the Azure Active Directory Domain Services. Keep checking back for updates.

### <a name="troubleshooting-guide"></a>Troubleshooting guide
Refer to our [Troubleshooting guide](active-directory-ds-troubleshooting.md) for solutions to common issues encountered when configuring or administering Azure AD Domain Services.

### <a name="configuration"></a>Configuration
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>Can I create multiple domains for a single Azure AD directory?
No. You can only create a single domain serviced by Azure AD Domain Services for a single Azure AD directory.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>Can I enable Azure AD Domain Services in an Azure Resource Manager virtual network?
No. Azure AD Domain Services can only be enabled in a classic Azure virtual network. You can connect the classic virtual network to a Resource Manager virtual network using virtual network peering to use your managed domain in a Resource Manager virtual network.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-to-authenticate-users-for-access-to-office-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>Can I enable Azure AD Domain Services in a federated Azure AD directory? I use ADFS to authenticate users for access to Office 365. Can I enable Azure AD Domain Services for this directory?
No. Azure AD Domain Services needs access to the password hashes of user accounts, to authenticate users via NTLM or Kerberos. In a federated directory, password hashes are not stored in the Azure AD directory. Therefore, Azure AD Domain Services does not work with such Azure AD directories.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>Can I make Azure AD Domain Services available in multiple virtual networks within my subscription?
The service itself does not directly support this scenario. Azure AD Domain Services is available in only one virtual network at a time. However, you may configure connectivity between multiple virtual networks to expose Azure AD Domain Services to other virtual networks. This article describes how you can [connect virtual networks in Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>Can I enable Azure AD Domain Services using PowerShell?
PowerShell/automated deployment of Azure AD Domain Services is not available currently.

#### <a name="is-azure-ad-domain-services-available-in-the-new-azure-portal"></a>Is Azure AD Domain Services available in the new Azure portal?
No. Azure AD Domain Services can be configured only in the [Azure classic portal](https://manage.windowsazure.com). We expect to extend support for the [Azure portal](https://portal.azure.com) in the future.

#### <a name="can-i-add-domain-controllers-to-an-azure-ad-domain-services-managed-domain"></a>Can I add domain controllers to an Azure AD Domain Services managed domain?
No. The domain provided by Azure AD Domain Services is a managed domain. You do not need to provision, configure, or otherwise manage domain controllers for this domain - these management activities are provided as a service by Microsoft. Therefore, you cannot add additional domain controllers (read-write or read-only) for the managed domain.

### <a name="administration-and-operations"></a>Administration and Operations
#### <a name="can-i-connect-to-the-domain-controller-for-my-managed-domain-using-remote-desktop"></a>Can I connect to the domain controller for my managed domain using Remote Desktop?
No. You do not have permissions to connect to domain controllers for the managed domain via Remote Desktop. Members of the 'AAD DC Administrators' group can administer the managed domain using AD administration tools such as the Active Directory Administration Center (ADAC) or AD PowerShell. These tools are installed using the 'Remote Server Administration Tools' feature on a Windows server joined to the managed domain.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-to-domain-join-machines-to-this-domain"></a>I’ve enabled Azure AD Domain Services. What user account do I use to domain join machines to this domain?
Members of the administrative group ‘AAD DC Administrators’ can domain-join machines. Additionally, members of this group are granted remote desktop access to machines that have been joined to the domain.

#### <a name="do-i-have-domain-administrator-privileges-for-the-managed-domain-provided-by-azure-ad-domain-services"></a>Do I have domain administrator privileges for the managed domain provided by Azure AD Domain Services?
No. You are not granted administrative privileges on the managed domain. Both ‘Domain Administrator’ and ‘Enterprise Administrator’ privileges are not available for you to use within the domain. Existing domain administrator or enterprise administrator groups within your Azure AD directory are also not granted domain/enterprise administrator privileges on the domain.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>Can I modify group memberships using LDAP or other AD administrative tools on managed domains?
No. Group memberships cannot be modified on domains serviced by Azure AD Domain Services. The same applies for user attributes. You may however change group memberships or user attributes either in Azure AD or on your on-premises domain. Such changes are automatically synchronized to Azure AD Domain Services.

#### <a name="how-long-does-it-take-for-changes-i-make-to-my-azure-ad-directory-to-be-visible-in-my-managed-domain"></a>How long does it take for changes I make to my Azure AD directory to be visible in my managed domain?
Changes made in your Azure AD directory using either the Azure AD UI or PowerShell are synchronized to your managed domain. This synchronization process runs in the background. After the one-time initial synchronization of your directory is complete, it typically takes about 20 minutes for changes made in Azure AD to be reflected in your managed domain.

#### <a name="can-i-extend-the-schema-of-the-managed-domain-provided-by-azure-ad-domain-services"></a>Can I extend the schema of the managed domain provided by Azure AD Domain Services?
No. The schema is administered by Microsoft for the managed domain. Schema extensions are not supported by Azure AD Domain Services.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>Can I modify or add DNS records in my managed domain?
Yes. Members of the 'AAD DC Administrators' group are granted 'DNS Administrator' privileges, to modify DNS records in the managed domain. They can use the DNS Manager console on a machine running Windows Server joined to the managed domain, to manage DNS. To use the DNS Manager console, install 'DNS Server Tools', which is part of the 'Remote Server Administration Tools' optional feature on the server. More information on [utilities for administering, monitoring and troubleshooting DNS](https://technet.microsoft.com/library/cc753579.aspx) is available on TechNet.

### <a name="billing-and-availability"></a>Billing and availability
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>Is Azure AD Domain Services a paid service?
Yes. For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/active-directory-ds/).

#### <a name="is-there-a-free-trial-for-the-service"></a>Is there a free trial for the service?
This service is included in the free trial for Azure. You can sign up for a [free one-month trial of Azure](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-to-use-azure-ad-domain-services"></a>Can I get Azure AD Domain Services as part of Enterprise Mobility Suite (EMS)? Do I need Azure AD Premium to use Azure AD Domain Services?
No. Azure AD Domain Services is a pay-as-you-go Azure service and is not part of EMS. Azure AD Domain Services can be used with all editions of Azure AD (Free, Basic, and, Premium). You are billed on an hourly basis, depending on usage.

#### <a name="what-azure-regions-is-the-service-available-in"></a>What Azure regions is the service available in?
Refer to the [Azure Services by region](https://azure.microsoft.com/regions/#services/) page to see a list of the Azure regions where Azure AD Domain Services is available.
