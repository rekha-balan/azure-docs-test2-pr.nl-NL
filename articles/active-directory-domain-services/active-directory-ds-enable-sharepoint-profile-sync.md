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
# <a name="configure-a-managed-domain-to-support-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="98a2c-103">Configure a managed domain to support profile synchronization for SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="98a2c-103">Configure a managed domain to support profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="98a2c-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span><span class="sxs-lookup"><span data-stu-id="98a2c-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="98a2c-105">To set up the User Profile Service, appropriate permissions need to be granted on an Active Directory domain.</span><span class="sxs-lookup"><span data-stu-id="98a2c-105">To set up the User Profile Service, appropriate permissions need to be granted on an Active Directory domain.</span></span> <span data-ttu-id="98a2c-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="98a2c-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="98a2c-107">This article explains how you can configure Azure AD Domain Services managed domains to deploy the SharePoint Server User Profile Sync service.</span><span class="sxs-lookup"><span data-stu-id="98a2c-107">This article explains how you can configure Azure AD Domain Services managed domains to deploy the SharePoint Server User Profile Sync service.</span></span>

## <a name="the-aad-dc-service-accounts-group"></a><span data-ttu-id="98a2c-108">The 'AAD DC Service Accounts' group</span><span class="sxs-lookup"><span data-stu-id="98a2c-108">The 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="98a2c-109">A security group called '**AAD DC Service Accounts**' is available within the 'Users' organizational unit on your managed domain.</span><span class="sxs-lookup"><span data-stu-id="98a2c-109">A security group called '**AAD DC Service Accounts**' is available within the 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="98a2c-110">You can see this group in the **Active Directory Users and Computers** MMC snap-in on your managed domain.</span><span class="sxs-lookup"><span data-stu-id="98a2c-110">You can see this group in the **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![AAD DC Service Accounts security group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="98a2c-112">Members of this security group are delegated the following privileges:</span><span class="sxs-lookup"><span data-stu-id="98a2c-112">Members of this security group are delegated the following privileges:</span></span>
- <span data-ttu-id="98a2c-113">The 'Replicate Directory Changes' privilege on the root DSE of the managed domain.</span><span class="sxs-lookup"><span data-stu-id="98a2c-113">The 'Replicate Directory Changes' privilege on the root DSE of the managed domain.</span></span>
- <span data-ttu-id="98a2c-114">The 'Replicate Directory Changes' privilege on the Configuration naming context (cn=configuration container) of the managed domain.</span><span class="sxs-lookup"><span data-stu-id="98a2c-114">The 'Replicate Directory Changes' privilege on the Configuration naming context (cn=configuration container) of the managed domain.</span></span>

<span data-ttu-id="98a2c-115">This security group is also a member of the built-in group **Pre-Windows 2000 Compatible Access**.</span><span class="sxs-lookup"><span data-stu-id="98a2c-115">This security group is also a member of the built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![AAD DC Service Accounts security group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-to-support-sharepoint-server-user-profile-sync"></a><span data-ttu-id="98a2c-117">Enable your managed domain to support SharePoint Server user profile sync</span><span class="sxs-lookup"><span data-stu-id="98a2c-117">Enable your managed domain to support SharePoint Server user profile sync</span></span>
<span data-ttu-id="98a2c-118">You can add the service account used for SharePoint user profile synchronization to the **AAD DC Service Accounts** group.</span><span class="sxs-lookup"><span data-stu-id="98a2c-118">You can add the service account used for SharePoint user profile synchronization to the **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="98a2c-119">As a result, the synchronization account gets adequate privileges to replicate changes to the directory.</span><span class="sxs-lookup"><span data-stu-id="98a2c-119">As a result, the synchronization account gets adequate privileges to replicate changes to the directory.</span></span> <span data-ttu-id="98a2c-120">This configuration step enables SharePoint Server user profile sync to work correctly.</span><span class="sxs-lookup"><span data-stu-id="98a2c-120">This configuration step enables SharePoint Server user profile sync to work correctly.</span></span>

![AAD DC Service Accounts - add members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![AAD DC Service Accounts - add members](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="98a2c-123">Related Content</span><span class="sxs-lookup"><span data-stu-id="98a2c-123">Related Content</span></span>
* [<span data-ttu-id="98a2c-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="98a2c-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)




