---
title: 'Azure Active Directory Domain Services: Enable password hash synchronization | Microsoft Docs'
description: Getting started with Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: ''
author: mahesh-unnikrishnan
manager: mtillman
editor: curtand
ms.assetid: 5a32a0df-a3ca-4ebe-b980-91f58f8030fc
ms.service: active-directory
ms.component: domain-services
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 04/02/2018
ms.author: maheshu
ms.openlocfilehash: 0f7023b60ef3678c284fe05bff7be73674595512
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44782423"
---
# <a name="enable-password-hash-synchronization-to-azure-active-directory-domain-services"></a><span data-ttu-id="652ba-103">Enable password hash synchronization to Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="652ba-103">Enable password hash synchronization to Azure Active Directory Domain Services</span></span>
<span data-ttu-id="652ba-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span><span class="sxs-lookup"><span data-stu-id="652ba-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="652ba-105">The next task is to enable synchronization of password hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="652ba-105">The next task is to enable synchronization of password hashes required for NT LAN Manager (NTLM) and Kerberos authentication to Azure AD Domain Services.</span></span> <span data-ttu-id="652ba-106">After you've set up password hash synchronization, users can sign in to the managed domain with their corporate credentials.</span><span class="sxs-lookup"><span data-stu-id="652ba-106">After you've set up password hash synchronization, users can sign in to the managed domain with their corporate credentials.</span></span>

<span data-ttu-id="652ba-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="652ba-107">The steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> 

<br>
| <span data-ttu-id="652ba-108">**Type of user account**</span><span class="sxs-lookup"><span data-stu-id="652ba-108">**Type of user account**</span></span> | <span data-ttu-id="652ba-109">**Steps to perform**</span><span class="sxs-lookup"><span data-stu-id="652ba-109">**Steps to perform**</span></span> |
| --- |---|
| <span data-ttu-id="652ba-110">**Cloud user accounts created in Azure AD**</span><span class="sxs-lookup"><span data-stu-id="652ba-110">**Cloud user accounts created in Azure AD**</span></span> |<span data-ttu-id="652ba-111">**&#x2713;** [Follow the instructions in this article](active-directory-ds-getting-started-password-sync.md#task-5-enable-password-hash-synchronization-to-your-managed-domain-for-cloud-only-user-accounts)</span><span class="sxs-lookup"><span data-stu-id="652ba-111">**&#x2713;** [Follow the instructions in this article](active-directory-ds-getting-started-password-sync.md#task-5-enable-password-hash-synchronization-to-your-managed-domain-for-cloud-only-user-accounts)</span></span> |
| <span data-ttu-id="652ba-112">**User accounts synchronized from an on-premises directory**</span><span class="sxs-lookup"><span data-stu-id="652ba-112">**User accounts synchronized from an on-premises directory**</span></span> |<span data-ttu-id="652ba-113">**&#x2713;** [Synchronize password hashes for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="652ba-113">**&#x2713;** [Synchronize password hashes for user accounts synced from your on-premises AD to your managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span> | 

<br>

> [!TIP]
> <span data-ttu-id="652ba-114">**You may need to complete both sets of steps.**</span><span class="sxs-lookup"><span data-stu-id="652ba-114">**You may need to complete both sets of steps.**</span></span>
> <span data-ttu-id="652ba-115">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to complete both sets of steps.</span><span class="sxs-lookup"><span data-stu-id="652ba-115">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need to complete both sets of steps.</span></span>
>

## <a name="task-5-enable-password-hash-synchronization-to-your-managed-domain-for-cloud-only-user-accounts"></a><span data-ttu-id="652ba-116">Task 5: enable password hash synchronization to your managed domain for cloud-only user accounts</span><span class="sxs-lookup"><span data-stu-id="652ba-116">Task 5: enable password hash synchronization to your managed domain for cloud-only user accounts</span></span>
<span data-ttu-id="652ba-117">To authenticate users on the managed domain, Azure Active Directory Domain Services needs password hashes in a format that's suitable for NTLM and Kerberos authentication.</span><span class="sxs-lookup"><span data-stu-id="652ba-117">To authenticate users on the managed domain, Azure Active Directory Domain Services needs password hashes in a format that's suitable for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="652ba-118">Azure AD does not generate or store password hashes in the format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span><span class="sxs-lookup"><span data-stu-id="652ba-118">Azure AD does not generate or store password hashes in the format that's required for NTLM or Kerberos authentication, until you enable Azure Active Directory Domain Services for your tenant.</span></span> <span data-ttu-id="652ba-119">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span><span class="sxs-lookup"><span data-stu-id="652ba-119">For obvious security reasons, Azure AD also does not store any password credentials in clear-text form.</span></span> <span data-ttu-id="652ba-120">Therefore, Azure AD does not have a way to automatically generate these NTLM or Kerberos password hashes based on users' existing credentials.</span><span class="sxs-lookup"><span data-stu-id="652ba-120">Therefore, Azure AD does not have a way to automatically generate these NTLM or Kerberos password hashes based on users' existing credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="652ba-121">**If your organization has cloud-only user accounts, all users who need to use Azure Active Directory Domain Services must change their passwords.**</span><span class="sxs-lookup"><span data-stu-id="652ba-121">**If your organization has cloud-only user accounts, all users who need to use Azure Active Directory Domain Services must change their passwords.**</span></span> <span data-ttu-id="652ba-122">A cloud-only user account is an account that was created in your Azure AD directory using either the Azure portal or Azure AD PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="652ba-122">A cloud-only user account is an account that was created in your Azure AD directory using either the Azure portal or Azure AD PowerShell cmdlets.</span></span> <span data-ttu-id="652ba-123">Such user accounts aren't synchronized from an on-premises directory.</span><span class="sxs-lookup"><span data-stu-id="652ba-123">Such user accounts aren't synchronized from an on-premises directory.</span></span>
>
>

<span data-ttu-id="652ba-124">This password change process causes the password hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication to be generated in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="652ba-124">This password change process causes the password hashes that are required by Azure Active Directory Domain Services for Kerberos and NTLM authentication to be generated in Azure AD.</span></span> <span data-ttu-id="652ba-125">You can either expire the passwords for all users in the tenant who need to use Azure Active Directory Domain Services or instruct them to change their passwords.</span><span class="sxs-lookup"><span data-stu-id="652ba-125">You can either expire the passwords for all users in the tenant who need to use Azure Active Directory Domain Services or instruct them to change their passwords.</span></span>

### <a name="enable-ntlm-and-kerberos-password-hash-generation-for-a-cloud-only-user-account"></a><span data-ttu-id="652ba-126">Enable NTLM and Kerberos password hash generation for a cloud-only user account</span><span class="sxs-lookup"><span data-stu-id="652ba-126">Enable NTLM and Kerberos password hash generation for a cloud-only user account</span></span>
<span data-ttu-id="652ba-127">Here are the instructions you need to provide users, so they can change their passwords:</span><span class="sxs-lookup"><span data-stu-id="652ba-127">Here are the instructions you need to provide users, so they can change their passwords:</span></span>

1. <span data-ttu-id="652ba-128">Go to the [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span><span class="sxs-lookup"><span data-stu-id="652ba-128">Go to the [Azure AD Access Panel](http://myapps.microsoft.com) page for your organization.</span></span>

    ![Launch the Azure AD access panel](./media/active-directory-domain-services-getting-started/access-panel.png)

2. <span data-ttu-id="652ba-130">In the top right corner, click on your name and select **Profile** from the menu.</span><span class="sxs-lookup"><span data-stu-id="652ba-130">In the top right corner, click on your name and select **Profile** from the menu.</span></span>

    ![Select profile](./media/active-directory-domain-services-getting-started/select-profile.png)

3. <span data-ttu-id="652ba-132">On the **Profile** page, click on **Change password**.</span><span class="sxs-lookup"><span data-stu-id="652ba-132">On the **Profile** page, click on **Change password**.</span></span>

    ![Click on "Change password"](./media/active-directory-domain-services-getting-started/user-change-password.png)

   > [!TIP]
   > <span data-ttu-id="652ba-134">If the **Change password** option is not displayed in the Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/authentication/quickstart-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="652ba-134">If the **Change password** option is not displayed in the Access Panel window, ensure that your organization has configured [password management in Azure AD](../active-directory/authentication/quickstart-sspr.md).</span></span>
   >
   >
4. <span data-ttu-id="652ba-135">On the **change password** page, type your existing (old) password, type a new password, and then confirm it.</span><span class="sxs-lookup"><span data-stu-id="652ba-135">On the **change password** page, type your existing (old) password, type a new password, and then confirm it.</span></span>

    ![User changes password](./media/active-directory-domain-services-getting-started/user-change-password2.png)

5. <span data-ttu-id="652ba-137">Click **submit**.</span><span class="sxs-lookup"><span data-stu-id="652ba-137">Click **submit**.</span></span>

<span data-ttu-id="652ba-138">A few minutes after you have changed your password, the new password is usable in Azure Active Directory Domain Services.</span><span class="sxs-lookup"><span data-stu-id="652ba-138">A few minutes after you have changed your password, the new password is usable in Azure Active Directory Domain Services.</span></span> <span data-ttu-id="652ba-139">After about 20 minutes, you can sign in to computers joined to the managed domain using the newly changed password.</span><span class="sxs-lookup"><span data-stu-id="652ba-139">After about 20 minutes, you can sign in to computers joined to the managed domain using the newly changed password.</span></span>

## <a name="related-content"></a><span data-ttu-id="652ba-140">Related Content</span><span class="sxs-lookup"><span data-stu-id="652ba-140">Related Content</span></span>
* [<span data-ttu-id="652ba-141">How to update your own password</span><span class="sxs-lookup"><span data-stu-id="652ba-141">How to update your own password</span></span>](../active-directory/user-help/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="652ba-142">Getting started with Password Management in Azure AD</span><span class="sxs-lookup"><span data-stu-id="652ba-142">Getting started with Password Management in Azure AD</span></span>](../active-directory/authentication/quickstart-sspr.md)
* [<span data-ttu-id="652ba-143">Enable password hash synchronization to Azure Active Directory Domain Services for a synced Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="652ba-143">Enable password hash synchronization to Azure Active Directory Domain Services for a synced Azure AD tenant</span></span>](active-directory-ds-getting-started-password-sync-synced-tenant.md)
* [<span data-ttu-id="652ba-144">Administer an Azure Active Directory Domain Services-managed domain</span><span class="sxs-lookup"><span data-stu-id="652ba-144">Administer an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="652ba-145">Join a Windows virtual machine to an Azure Active Directory Domain Services-managed domain</span><span class="sxs-lookup"><span data-stu-id="652ba-145">Join a Windows virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="652ba-146">Join a Red Hat Enterprise Linux virtual machine to an Azure Active Directory Domain Services-managed domain</span><span class="sxs-lookup"><span data-stu-id="652ba-146">Join a Red Hat Enterprise Linux virtual machine to an Azure Active Directory Domain Services-managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
