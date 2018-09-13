---
title: Upgrade from DirSync and Azure AD Sync | Microsoft Docs
description: Describes how to upgrade from DirSync and Azure AD Sync to Azure AD Connect.
services: active-directory
documentationcenter: ''
author: andkjell
manager: femila
editor: ''
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cd11ef761a39b47e2426766cba64b3975595f4d4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550916"
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>Upgrade Windows Azure Active Directory Sync and Azure Active Directory Sync
Azure AD Connect is the best way to connect your on-premises directory with Azure AD and Office 365. This is a great time to upgrade to Azure AD Connect from Windows Azure Active Directory Sync (DirSync) or Azure AD Sync as these tools are now deprecated and will reach end of support on April 13, 2017.

The two identity synchronization tools that are deprecated were offered for single forest customers (DirSync) and for multi-forest and other advanced customers (Azure AD Sync). These older tools have been replaced with a single solution that is available for all scenarios: Azure AD Connect. It offers new functionality, feature enhancements, and support for new scenarios. To be able to continue to synchronize your on-premises identity data to Azure AD and Office 365, we strongly recommend that you upgrade to Azure AD Connect.

The last release of DirSync was released in July 2014 and the last release of Azure AD Sync was released in May 2015.

## <a name="what-is-azure-ad-connect"></a>What is Azure AD Connect
Azure AD Connect is the successor to DirSync and Azure AD Sync. It combines all scenarios these two supported. You can read more about it in [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).

## <a name="deprecation-schedule"></a>Deprecation schedule
| Date | Comment |
| --- | --- |
| April 13, 2016 |Windows Azure Active Directory Sync (“DirSync”) and Microsoft Azure Active Directory Sync (“Azure AD Sync”) are announced as deprecated. |
| April 13, 2017 |Support ends. Customers will no longer be able to open a support case without upgrading to Azure AD Connect first. |
|December 31, 2017|Azure AD will no longer accept communications from Windows Azure Active Directory Sync (“DirSync”) and Microsoft Azure Active Directory Sync (“Azure AD Sync”).

## <a name="how-to-transition-to-azure-ad-connect"></a>How to transition to Azure AD Connect
If you are running DirSync, there are two ways you can upgrade: In-place upgrade and parallel deployment. An in-place upgrade is recommended for most customers and if you have a recent operating system and less than 50,000 objects. In other cases, it is recommended to do a parallel deployment where your DirSync configuration is moved to a new server running Azure AD Connect.

If you use Azure AD Sync, then an in-place upgrade is recommended. If you want to, it is possible to install a new Azure AD Connect server in parallel and do a swing migration from your Azure AD Sync server to Azure AD Connect.

| Solution | Scenario |
| --- | --- |
| [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>If you have an existing DirSync server already running.</li> |
| [Upgrade from Azure AD Sync](active-directory-aadconnect-upgrade-previous-version.md) |<li>If you are moving from Azure AD Sync.</li> |

If you want to see how to do an in-place upgrade from DirSync to Azure AD Connect, then see this Channel 9 video:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>FAQ
**Q: I have received an email notification from the Azure Team and/or a message from the Office 365 message center, but I am using Connect.**  
The notification was also sent to customers using Azure AD Connect with a build number 1.0.\*.0 (using a pre-1.1 release). Microsoft recommends customers to stay current with Azure AD Connect releases. The [automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) feature introduced in 1.1 makes it easy to always have a recent version of Azure AD Connect installed.

**Q: Will DirSync/Azure AD Sync stop working on April 13, 2017?**  
DirSync/Azure AD Sync will continue to work on April 13th 2017.  However, Azure AD will no longer accept communications from DirSync/Azure AD Sync on December 31st 2017.

**Q: Which DirSync versions can I upgrade from?**  
It is supported to upgrade from any DirSync release currently being used.

**Q: What about the Azure AD Connector for FIM/MIM?**  
The Azure AD Connector for FIM/MIM has **not** been announced as deprecated. It is at **feature freeze**; no new functionality is added and it receives no bug fixes. Microsoft recommends customers using it to plan to move from it to Azure AD Connect. It is strongly recommended to not start any new deployments using it. This Connector will be announced deprecated in the future.

## <a name="additional-resources"></a>Additional Resources
* [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md)