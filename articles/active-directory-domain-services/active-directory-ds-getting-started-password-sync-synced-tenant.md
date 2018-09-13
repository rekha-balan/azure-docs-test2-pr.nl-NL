---
title: 'Azure AD Domain Services: Enable password synchronization | Microsoft Docs'
description: Getting started with Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 4969b43831a3813a4e76c6447c252a9c458f371a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563606"
---
# <a name="enable-password-synchronization-to-azure-ad-domain-services"></a><span data-ttu-id="989ef-103">Enable password synchronization to Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="989ef-103">Enable password synchronization to Azure AD Domain Services</span></span>
<span data-ttu-id="989ef-104">In preceding tasks, you enabled Azure AD Domain Services for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="989ef-104">In preceding tasks, you enabled Azure AD Domain Services for your Azure AD tenant.</span></span> <span data-ttu-id="989ef-105">The next task is to enable synchronization of passwords to Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="989ef-105">The next task is to enable synchronization of passwords to Azure AD Domain Services.</span></span> <span data-ttu-id="989ef-106">Once credential synchronization is set up, users can sign in to the managed domain using their corporate credentials.</span><span class="sxs-lookup"><span data-stu-id="989ef-106">Once credential synchronization is set up, users can sign in to the managed domain using their corporate credentials.</span></span>

<span data-ttu-id="989ef-107">The steps involved are different based on whether your organization has a cloud-only Azure AD tenant or is set to synchronize with your on-premises directory using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="989ef-107">The steps involved are different based on whether your organization has a cloud-only Azure AD tenant or is set to synchronize with your on-premises directory using Azure AD Connect.</span></span>

<br>

> [!div class="op_single_selector"]
> * [Cloud-only Azure AD tenant](active-directory-ds-getting-started-password-sync.md)
> * [Synced Azure AD tenant](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

<br>

## <a name="task-5-enable-password-synchronization-to-aad-domain-services-for-a-synced-azure-ad-tenant"></a><span data-ttu-id="989ef-110">Task 5: Enable password synchronization to AAD Domain Services for a synced Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="989ef-110">Task 5: Enable password synchronization to AAD Domain Services for a synced Azure AD tenant</span></span>
<span data-ttu-id="989ef-111">A synced Azure AD tenant is set to synchronize with your organization's on-premises directory using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="989ef-111">A synced Azure AD tenant is set to synchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="989ef-112">Azure AD Connect does not synchronize NTLM and Kerberos credential hashes to Azure AD by default.</span><span class="sxs-lookup"><span data-stu-id="989ef-112">Azure AD Connect does not synchronize NTLM and Kerberos credential hashes to Azure AD by default.</span></span> <span data-ttu-id="989ef-113">To use Azure AD Domain Services, you need to configure Azure AD Connect to synchronize credential hashes required for NTLM and Kerberos authentication.</span><span class="sxs-lookup"><span data-stu-id="989ef-113">To use Azure AD Domain Services, you need to configure Azure AD Connect to synchronize credential hashes required for NTLM and Kerberos authentication.</span></span> 

> [!WARNING]
> You MUST enable password synchronization to AAD Domain Services every time you enable Azure AD Domain Services. You may have previously enabled Azure AD Domain Services for your Azure AD directory and then turned if off. However, you must still enable password synchronization the next time you enable Azure AD Domain Services for the directory.
>
>

<span data-ttu-id="989ef-117">The following steps enable synchronization of the required credential hashes to your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="989ef-117">The following steps enable synchronization of the required credential hashes to your Azure AD tenant.</span></span>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="989ef-118">Install or update Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="989ef-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="989ef-119">Install the latest recommended release of Azure AD Connect on a domain joined computer.</span><span class="sxs-lookup"><span data-stu-id="989ef-119">Install the latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="989ef-120">If you have an existing instance of Azure AD Connect setup, you need to update it to use the latest version of Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="989ef-120">If you have an existing instance of Azure AD Connect setup, you need to update it to use the latest version of Azure AD Connect.</span></span> <span data-ttu-id="989ef-121">To avoid known issues/bugs that may have already been fixed, ensure you always use the latest version of Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="989ef-121">To avoid known issues/bugs that may have already been fixed, ensure you always use the latest version of Azure AD Connect.</span></span>

<span data-ttu-id="989ef-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="989ef-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="989ef-123">Recommended version: **1.1.281.0** - published on September 7, 2016.</span><span class="sxs-lookup"><span data-stu-id="989ef-123">Recommended version: **1.1.281.0** - published on September 7, 2016.</span></span>

> [!WARNING]
> You MUST install the latest recommended release of Azure AD Connect to enable the legacy password credentials (required for NTLM and Kerberos authentication) to synchronize to your Azure AD tenant. This functionality is not available in prior releases of Azure AD Connect or with the legacy DirSync tool.
>
>

<span data-ttu-id="989ef-126">Installation instructions for Azure AD Connect are available in the following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="989ef-126">Installation instructions for Azure AD Connect are available in the following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-to-azure-ad"></a><span data-ttu-id="989ef-127">Enable synchronization of NTLM and Kerberos credential hashes to Azure AD</span><span class="sxs-lookup"><span data-stu-id="989ef-127">Enable synchronization of NTLM and Kerberos credential hashes to Azure AD</span></span>
<span data-ttu-id="989ef-128">Execute the following PowerShell script on each AD forest, to force full password synchronization, and enable all on-premises users’ credential hashes to sync to your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="989ef-128">Execute the following PowerShell script on each AD forest, to force full password synchronization, and enable all on-premises users’ credential hashes to sync to your Azure AD tenant.</span></span> <span data-ttu-id="989ef-129">This script enables the credential hashes required for NTLM/Kerberos authentication to be synchronized to your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="989ef-129">This script enables the credential hashes required for NTLM/Kerberos authentication to be synchronized to your Azure AD tenant.</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

<span data-ttu-id="989ef-130">Depending on the size of your directory (number of users, groups etc.), synchronization of credential hashes to Azure AD takes time.</span><span class="sxs-lookup"><span data-stu-id="989ef-130">Depending on the size of your directory (number of users, groups etc.), synchronization of credential hashes to Azure AD takes time.</span></span> <span data-ttu-id="989ef-131">The passwords will be usable on the Azure AD Domain Services managed domain shortly after the credential hashes have synchronized to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="989ef-131">The passwords will be usable on the Azure AD Domain Services managed domain shortly after the credential hashes have synchronized to Azure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="989ef-132">Related Content</span><span class="sxs-lookup"><span data-stu-id="989ef-132">Related Content</span></span>
* [<span data-ttu-id="989ef-133">Enable password synchronization to AAD Domain Services for a cloud-only Azure AD directory</span><span class="sxs-lookup"><span data-stu-id="989ef-133">Enable password synchronization to AAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="989ef-134">Administer an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="989ef-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="989ef-135">Join a Windows virtual machine to an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="989ef-135">Join a Windows virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="989ef-136">Join a Red Hat Enterprise Linux virtual machine to an Azure AD Domain Services managed domain</span><span class="sxs-lookup"><span data-stu-id="989ef-136">Join a Red Hat Enterprise Linux virtual machine to an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
