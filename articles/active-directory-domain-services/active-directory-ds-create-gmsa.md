---
title: 'Azure Active Directory Domain Services: Create a group managed service account | Microsoft Docs'
description: Administer Azure Active Directory Domain Services managed domains
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: e6faeddd-ef9e-4e23-84d6-c9b3f7d16567
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/26/2018
ms.author: maheshu
ms.openlocfilehash: 9bfd38b2eba3cab5012e5715ad283b9cb7b84a9b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867922"
---
# <a name="create-a-group-managed-service-account-gmsa-on-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="a37ba-103">Create a group managed service account (gMSA) on an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="a37ba-103">Create a group managed service account (gMSA) on an Azure AD Domain Services managed domain</span></span>
<span data-ttu-id="a37ba-104">This article shows you how to create managed service accounts on an Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="a37ba-104">This article shows you how to create managed service accounts on an Azure AD Domain Services managed domain.</span></span>

## <a name="managed-service-accounts"></a><span data-ttu-id="a37ba-105">Managed Service Accounts</span><span class="sxs-lookup"><span data-stu-id="a37ba-105">Managed Service Accounts</span></span>
<span data-ttu-id="a37ba-106">A standalone-Managed Service Account (sMSA) is a managed domain account whose password is automatically managed.</span><span class="sxs-lookup"><span data-stu-id="a37ba-106">A standalone-Managed Service Account (sMSA) is a managed domain account whose password is automatically managed.</span></span> <span data-ttu-id="a37ba-107">It simplifies service principal name (SPN) management, and enables delegated management to other administrators.</span><span class="sxs-lookup"><span data-stu-id="a37ba-107">It simplifies service principal name (SPN) management, and enables delegated management to other administrators.</span></span> <span data-ttu-id="a37ba-108">This type of managed service account (MSA) was introduced in Windows Server 2008 R2 and Windows 7.</span><span class="sxs-lookup"><span data-stu-id="a37ba-108">This type of managed service account (MSA) was introduced in Windows Server 2008 R2 and Windows 7.</span></span>

<span data-ttu-id="a37ba-109">The group-Managed Service Account (gMSA) provides the same benefits for many servers on the domain.</span><span class="sxs-lookup"><span data-stu-id="a37ba-109">The group-Managed Service Account (gMSA) provides the same benefits for many servers on the domain.</span></span> <span data-ttu-id="a37ba-110">All instances of a service hosted on a server farm need to use the same service principal for mutual authentication protocols to work.</span><span class="sxs-lookup"><span data-stu-id="a37ba-110">All instances of a service hosted on a server farm need to use the same service principal for mutual authentication protocols to work.</span></span> <span data-ttu-id="a37ba-111">When a gMSA is used as service principal, the Windows operating system manages the account's password instead of relying on the administrator.</span><span class="sxs-lookup"><span data-stu-id="a37ba-111">When a gMSA is used as service principal, the Windows operating system manages the account's password instead of relying on the administrator.</span></span>

<span data-ttu-id="a37ba-112">**More information:**</span><span class="sxs-lookup"><span data-stu-id="a37ba-112">**More information:**</span></span>
- [<span data-ttu-id="a37ba-113">Group Managed Service Accounts Overview</span><span class="sxs-lookup"><span data-stu-id="a37ba-113">Group Managed Service Accounts Overview</span></span>](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview)
- [<span data-ttu-id="a37ba-114">Getting started with Group Managed Service Accounts</span><span class="sxs-lookup"><span data-stu-id="a37ba-114">Getting started with Group Managed Service Accounts</span></span>](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts)


## <a name="using-service-accounts-in-azure-ad-domain-services"></a><span data-ttu-id="a37ba-115">Using service accounts in Azure AD Domain services</span><span class="sxs-lookup"><span data-stu-id="a37ba-115">Using service accounts in Azure AD Domain services</span></span>
<span data-ttu-id="a37ba-116">Azure AD Domain Services managed domains are locked down and managed by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a37ba-116">Azure AD Domain Services managed domains are locked down and managed by Microsoft.</span></span> <span data-ttu-id="a37ba-117">There are a couple of key considerations when using service accounts with Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="a37ba-117">There are a couple of key considerations when using service accounts with Azure AD Domain Services.</span></span>

### <a name="create-service-accounts-within-custom-organizational-units-ou-on-the-managed-domain"></a><span data-ttu-id="a37ba-118">Create service accounts within custom organizational units (OU) on the managed domain</span><span class="sxs-lookup"><span data-stu-id="a37ba-118">Create service accounts within custom organizational units (OU) on the managed domain</span></span>
<span data-ttu-id="a37ba-119">You can't create a service account in the built-in 'AADDC Users' or 'AADDC Computers' organizational units.</span><span class="sxs-lookup"><span data-stu-id="a37ba-119">You can't create a service account in the built-in 'AADDC Users' or 'AADDC Computers' organizational units.</span></span> <span data-ttu-id="a37ba-120">[Create a custom OU](active-directory-ds-admin-guide-create-ou.md) on your managed domain and then create service accounts within that custom OU.</span><span class="sxs-lookup"><span data-stu-id="a37ba-120">[Create a custom OU](active-directory-ds-admin-guide-create-ou.md) on your managed domain and then create service accounts within that custom OU.</span></span>

### <a name="the-key-distribution-services-kds-root-key-is-already-pre-created"></a><span data-ttu-id="a37ba-121">The Key Distribution Services (KDS) root key is already pre-created</span><span class="sxs-lookup"><span data-stu-id="a37ba-121">The Key Distribution Services (KDS) root key is already pre-created</span></span>
<span data-ttu-id="a37ba-122">The Key Distribution Services (KDS) root key is pre-created on an Azure AD Domain Services managed domain.</span><span class="sxs-lookup"><span data-stu-id="a37ba-122">The Key Distribution Services (KDS) root key is pre-created on an Azure AD Domain Services managed domain.</span></span> <span data-ttu-id="a37ba-123">You don't need to create a KDS root key and don't have privileges to do so either.</span><span class="sxs-lookup"><span data-stu-id="a37ba-123">You don't need to create a KDS root key and don't have privileges to do so either.</span></span> <span data-ttu-id="a37ba-124">You can't view the KDS root key on the managed domain either.</span><span class="sxs-lookup"><span data-stu-id="a37ba-124">You can't view the KDS root key on the managed domain either.</span></span>

## <a name="sample---create-a-gmsa-using-powershell"></a><span data-ttu-id="a37ba-125">Sample - create a gMSA using PowerShell</span><span class="sxs-lookup"><span data-stu-id="a37ba-125">Sample - create a gMSA using PowerShell</span></span>
<span data-ttu-id="a37ba-126">The following sample shows you how to create a custom OU using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a37ba-126">The following sample shows you how to create a custom OU using PowerShell.</span></span> <span data-ttu-id="a37ba-127">You can then create a gMSA within that OU by using the ```-Path``` parameter to specify the OU.</span><span class="sxs-lookup"><span data-stu-id="a37ba-127">You can then create a gMSA within that OU by using the ```-Path``` parameter to specify the OU.</span></span>

```powershell
# Create a new custom OU on the managed domain
New-ADOrganizationalUnit -Name "MyNewOU" -Path "DC=CONTOSO100,DC=COM"

# Create a service account 'WebFarmSvc' within the custom OU.
New-ADServiceAccount -Name WebFarmSvc  `
-DNSHostName ` WebFarmSvc.contoso100.com  `
-Path "OU=MYNEWOU,DC=CONTOSO100,DC=com"  `
-KerberosEncryptionType AES128, AES256  ` -ManagedPasswordIntervalInDays 30  `
-ServicePrincipalNames http/WebFarmSvc.contoso100.com/contoso100.com, `
http/WebFarmSvc.contoso100.com/contoso100,  `
http/WebFarmSvc/contoso100.com, http/WebFarmSvc/contoso100  `
-PrincipalsAllowedToRetrieveManagedPassword CONTOSO-SERVER$
```

<span data-ttu-id="a37ba-128">**PowerShell cmdlet documentation:**</span><span class="sxs-lookup"><span data-stu-id="a37ba-128">**PowerShell cmdlet documentation:**</span></span>
- [<span data-ttu-id="a37ba-129">New-ADOrganizationalUnit cmdlet</span><span class="sxs-lookup"><span data-stu-id="a37ba-129">New-ADOrganizationalUnit cmdlet</span></span>](https://docs.microsoft.com/powershell/module/addsadministration/new-adorganizationalunit)
- [<span data-ttu-id="a37ba-130">New-ADServiceAccount cmdlet</span><span class="sxs-lookup"><span data-stu-id="a37ba-130">New-ADServiceAccount cmdlet</span></span>](https://docs.microsoft.com/powershell/module/addsadministration/New-ADServiceAccount)


## <a name="next-steps"></a><span data-ttu-id="a37ba-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="a37ba-131">Next steps</span></span>
- [<span data-ttu-id="a37ba-132">Create a custom OU on a managed domain</span><span class="sxs-lookup"><span data-stu-id="a37ba-132">Create a custom OU on a managed domain</span></span>](active-directory-ds-admin-guide-create-ou.md)
- [<span data-ttu-id="a37ba-133">Group Managed Service Accounts Overview</span><span class="sxs-lookup"><span data-stu-id="a37ba-133">Group Managed Service Accounts Overview</span></span>](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview)
- [<span data-ttu-id="a37ba-134">Getting started with Group Managed Service Accounts</span><span class="sxs-lookup"><span data-stu-id="a37ba-134">Getting started with Group Managed Service Accounts</span></span>](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts)
