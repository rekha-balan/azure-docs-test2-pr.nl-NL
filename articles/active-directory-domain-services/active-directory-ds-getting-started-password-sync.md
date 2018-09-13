---
title: 'Azure Active Directory Domain Services: Enable password synchronization | Microsoft Docs'
description: Getting started with Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 439f97305e2cf2a40a659b6d13230af3df415d56
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563540"
---
# <a name="enable-password-synchronization-with-azure-active-directory-domain-services"></a><span data-ttu-id="7ae84-103">Enable password synchronization with Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="7ae84-103">Enable password synchronization with Azure Active Directory Domain Services</span></span>
<span data-ttu-id="7ae84-104">In the preceding tasks, you enabled Azure Active Directory Domain Services (AD DS) for your Azure Active Directory (Azure AD) tenant.</span><span class="sxs-lookup"><span data-stu-id="7ae84-104">In the preceding tasks, you enabled Azure Active Directory Domain Services (AD DS) for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="7ae84-105">The next task is to enable credential hashes, which are required for NT LAN Manager (NTLM) and Kerberos authentication to sync with Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="7ae84-105">The next task is to enable credential hashes, which are required for NT LAN Manager (NTLM) and Kerberos authentication to sync with Azure Active Directory Domain Services.</span></span> <span data-ttu-id="7ae84-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span><span class="sxs-lookup"><span data-stu-id="7ae84-106">After you've set up credential synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="7ae84-107">The procedures vary depending on whether your organization has a cloud-only Azure AD tenant or is set to sync with your on-premises directory by using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="7ae84-107">The procedures vary depending on whether your organization has a cloud-only Azure AD tenant or is set to sync with your on-premises directory by using Azure AD Connect.</span></span>

> [!div class="op_single_selector"]
> * [Cloud-only Azure AD tenant](active-directory-ds-getting-started-password-sync.md)
> * [Synced Azure AD tenant](active-directory-ds-getting-started-password-sync-synced-tenant.md)
>
>

## <a name="task-5-enable-password-synchronization-with-azure-active-directory-domain-services-for-a-cloud-only-azure-ad-tenant"></a><span data-ttu-id="7ae84-110">Task 5: Enable password synchronization with Azure Active Directory Domain Services for a cloud-only Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="7ae84-110">Task 5: Enable password synchronization with Azure Active Directory Domain Services for a cloud-only Azure AD tenant</span></span>
<span data-ttu-id="7ae84-111">To authenticate users on the managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span><span class="sxs-lookup"><span data-stu-id="7ae84-111">To authenticate users on the managed domain, Azure Active Directory Domain Services needs credential hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="7ae84-112">Unless you enable Azure Active Directory Domain Services for your tenant, Azure AD does not generate or store credential hashes in the format that's required for NTLM or Kerberos authentication.</span><span class="sxs-lookup"><span data-stu-id="7ae84-112">Unless you enable Azure Active Directory Domain Services for your tenant, Azure AD does not generate or store credential hashes in the format that's required for NTLM or Kerberos authentication.</span></span> <span data-ttu-id="7ae84-113">For obvious security reasons, Azure AD also does not store any credentials in clear-text form.</span><span class="sxs-lookup"><span data-stu-id="7ae84-113">For obvious security reasons, Azure AD also does not store any credentials in clear-text form.</span></span> <span data-ttu-id="7ae84-114">Therefore, Azure AD does not have a way to generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span><span class="sxs-lookup"><span data-stu-id="7ae84-114">Therefore, Azure AD does not have a way to generate these NTLM or Kerberos credential hashes based on users' existing credentials.</span></span>

> [!NOTE]
> If your organization has a cloud-only Azure AD tenant, users who need to use Azure Active Directory Domain Services must change their passwords.
>
>

<span data-ttu-id="7ae84-116">This password change process causes the credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication to be generated in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ae84-116">This password change process causes the credential hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication to be generated in Azure AD.</span></span> <span data-ttu-id="7ae84-117">You can either expire the passwords for all users in the tenant who need to use Azure Active Directory Domain Services or instruct them to change their passwords.</span><span class="sxs-lookup"><span data-stu-id="7ae84-117">You can either expire the passwords for all users in the tenant who need to use Azure Active Directory Domain Services or instruct them to change their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-credential-hash-generation-for-a-cloud-only-azure-ad-tenant"></a><span data-ttu-id="7ae84-118">Enable NTLM and Kerberos credential hash generation for a cloud-only Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="7ae84-118">Enable NTLM and Kerberos credential hash generation for a cloud-only Azure AD tenant</span></span>
<span data-ttu-id="7ae84-119">Here are the instructions you need to provide users, so they can change their passwords:</span><span class="sxs-lookup"><span data-stu-id="7ae84-119">Here are the instructions you need to provide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="7ae84-120">Go to the [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span><span class="sxs-lookup"><span data-stu-id="7ae84-120">Go to the [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>
2. <span data-ttu-id="7ae84-121">In the Access Panel window, select the **profile** tab.</span><span class="sxs-lookup"><span data-stu-id="7ae84-121">In the Access Panel window, select the **profile** tab.</span></span>
3. <span data-ttu-id="7ae84-122">Click the **Change password** tile.</span><span class="sxs-lookup"><span data-stu-id="7ae84-122">Click the **Change password** tile.</span></span>

    ![The Azure AD Access Panel "Change password" tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!NOTE]
   > If the **Change password** option is not displayed in the Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/active-directory-passwords-getting-started.md).
   >
   >
4. <span data-ttu-id="7ae84-125">On the **change password** page, type your existing (old) password, type a new password, and then confirm it.</span><span class="sxs-lookup"><span data-stu-id="7ae84-125">On the **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![Create a virtual network for Azure AD Domain Services.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory-domain-services/media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="7ae84-127">Click **submit**.</span><span class="sxs-lookup"><span data-stu-id="7ae84-127">Click **submit**.</span></span>

<span data-ttu-id="7ae84-128">A few minutes after you have changed your password, the new password is usable in Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="7ae84-128">A few minutes after you have changed your password, the new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="7ae84-129">After a few more minutes (typically, about 20 minutes), you can sign in to computers that are joined to the managed domain by using the newly changed password.</span><span class="sxs-lookup"><span data-stu-id="7ae84-129">After a few more minutes (typically, about 20 minutes), you can sign in to computers that are joined to the managed domain by using the newly changed password.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ae84-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ae84-130">Next steps</span></span>
* [<span data-ttu-id="7ae84-131">How to update your own password</span><span class="sxs-lookup"><span data-stu-id="7ae84-131">How to update your own password</span></span>](../active-directory/active-directory-passwords-update-your-own-password.md#reset-my-password)
* [<span data-ttu-id="7ae84-132">Getting started with Password Management in Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ae84-132">Getting started with Password Management in Azure AD</span></span>](../active-directory/active-directory-passwords-getting-started.md)
* [<span data-ttu-id="7ae84-133">Enable password synchronization to Azure Active Directory Domain Services for a synced Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="7ae84-133">Enable password synchronization to Azure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="7ae84-134">Administer an Azure Active Directory Domain Services-managed domain</span><span class="sxs-lookup"><span data-stu-id="7ae84-134">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="7ae84-135">Join a Windows virtual machine to an Azure Active Directory Domain Services-managed domain</span><span class="sxs-lookup"><span data-stu-id="7ae84-135">Join a Windows virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="7ae84-136">Join a Red Hat Enterprise Linux virtual machine to an Azure Active Directory Domain Services-managed domain</span><span class="sxs-lookup"><span data-stu-id="7ae84-136">Join a Red Hat Enterprise Linux virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)


