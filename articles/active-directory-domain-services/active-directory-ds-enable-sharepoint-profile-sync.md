---
title: 'Azure Active Directory Domain Services: Enable support for SharePoint User Profile service | Microsoft Docs'
description: Configure Azure Active Directory Domain Services managed domains to support profile synchronization for SharePoint Server
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 3aaabdc2286cda2b8f64a732ba49045f008bee18
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669175"
---
# <a name="configure-a-managed-domain-to-support-profile-synchronization-for-sharepoint-server"></a>Configure a managed domain to support profile synchronization for SharePoint Server
SharePoint Server includes a User Profile Service that is used for user profile synchronization. To set up the User Profile Service, appropriate permissions need to be granted on an Active Directory domain. For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).

This article explains how you can configure Azure AD Domain Services managed domains to deploy the SharePoint Server User Profile Sync service.

## <a name="the-aad-dc-service-accounts-group"></a>The 'AAD DC Service Accounts' group
A security group called '**AAD DC Service Accounts**' is available within the 'Users' organizational unit on your managed domain. You can see this group in the **Active Directory Users and Computers** MMC snap-in on your managed domain.

![AAD DC Service Accounts security group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

Members of this security group are delegated the following privileges:
- The 'Replicate Directory Changes' privilege on the root DSE of the managed domain.
- The 'Replicate Directory Changes' privilege on the Configuration naming context (cn=configuration container) of the managed domain.

This security group is also a member of the built-in group **Pre-Windows 2000 Compatible Access**.

![AAD DC Service Accounts security group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-to-support-sharepoint-server-user-profile-sync"></a>Enable your managed domain to support SharePoint Server user profile sync
You can add the service account used for SharePoint user profile synchronization to the **AAD DC Service Accounts** group. As a result, the synchronization account gets adequate privileges to replicate changes to the directory. This configuration step enables SharePoint Server user profile sync to work correctly.

![AAD DC Service Accounts - add members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC Service Accounts - add members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a>Related Content
* [Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx)




