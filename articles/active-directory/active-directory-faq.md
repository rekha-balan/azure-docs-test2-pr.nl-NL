---
title: Azure Active Directory FAQ | Microsoft Docs
description: Azure Active Directory FAQ answers questions about how to access Azure and Azure Active Directory, password management, and application access.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/07/2017
ms.author: markvi
ms.openlocfilehash: 025e8c9e575123a3ad9863a35061ebd0af212486
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551982"
---
# <a name="azure-active-directory-faq"></a><span data-ttu-id="d9614-103">Azure Active Directory FAQ</span><span class="sxs-lookup"><span data-stu-id="d9614-103">Azure Active Directory FAQ</span></span>
<span data-ttu-id="d9614-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span><span class="sxs-lookup"><span data-stu-id="d9614-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span></span>

<span data-ttu-id="d9614-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9614-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span></span>


## <a name="access-azure-and-azure-active-directory"></a><span data-ttu-id="d9614-106">Access Azure and Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9614-106">Access Azure and Azure Active Directory</span></span>
<span data-ttu-id="d9614-107">**Q: Why do I get “No subscriptions found” when I try to access Azure AD in the Azure classic portal (https://manage.windowsazure.com)?**</span><span class="sxs-lookup"><span data-stu-id="d9614-107">**Q: Why do I get “No subscriptions found” when I try to access Azure AD in the Azure classic portal (https://manage.windowsazure.com)?**</span></span>

<span data-ttu-id="d9614-108">**A:** To access the Azure classic portal, each user needs permissions with an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d9614-108">**A:** To access the Azure classic portal, each user needs permissions with an Azure subscription.</span></span> <span data-ttu-id="d9614-109">If you have a paid Office 365 or Azure AD subscription, go to [http://aka.ms/accessAAD](http://aka.ms/accessAAD) for a one-time activation step.</span><span class="sxs-lookup"><span data-stu-id="d9614-109">If you have a paid Office 365 or Azure AD subscription, go to [http://aka.ms/accessAAD](http://aka.ms/accessAAD) for a one-time activation step.</span></span> <span data-ttu-id="d9614-110">Otherwise, you will need to activate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span><span class="sxs-lookup"><span data-stu-id="d9614-110">Otherwise, you will need to activate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span></span>

<span data-ttu-id="d9614-111">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="d9614-111">For more information, see:</span></span>

* [<span data-ttu-id="d9614-112">How Azure subscriptions are associated with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9614-112">How Azure subscriptions are associated with Azure Active Directory</span></span>](active-directory-how-subscriptions-associated-directory.md)
* [<span data-ttu-id="d9614-113">Manage the directory for your Office 365 subscription in Azure</span><span class="sxs-lookup"><span data-stu-id="d9614-113">Manage the directory for your Office 365 subscription in Azure</span></span>](active-directory-manage-o365-subscription.md)

- - -
<span data-ttu-id="d9614-114">**Q: What’s the relationship between Azure AD, Office 365, and Azure?**</span><span class="sxs-lookup"><span data-stu-id="d9614-114">**Q: What’s the relationship between Azure AD, Office 365, and Azure?**</span></span>

<span data-ttu-id="d9614-115">**A:** Azure AD provides you with common identity and access capabilities to all web services.</span><span class="sxs-lookup"><span data-stu-id="d9614-115">**A:** Azure AD provides you with common identity and access capabilities to all web services.</span></span> <span data-ttu-id="d9614-116">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD to help turn on sign-on and access management for all these services.</span><span class="sxs-lookup"><span data-stu-id="d9614-116">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD to help turn on sign-on and access management for all these services.</span></span>

<span data-ttu-id="d9614-117">All users who are set up to use web services are defined as user accounts in one or more Azure AD instances.</span><span class="sxs-lookup"><span data-stu-id="d9614-117">All users who are set up to use web services are defined as user accounts in one or more Azure AD instances.</span></span> <span data-ttu-id="d9614-118">You can set up these accounts for free Azure AD capabilities like cloud application access.</span><span class="sxs-lookup"><span data-stu-id="d9614-118">You can set up these accounts for free Azure AD capabilities like cloud application access.</span></span>

<span data-ttu-id="d9614-119">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span><span class="sxs-lookup"><span data-stu-id="d9614-119">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span></span>
- - -
<span data-ttu-id="d9614-120">**Q:  Why can I sign in to the Azure portal but not the Azure classic portal?**</span><span class="sxs-lookup"><span data-stu-id="d9614-120">**Q:  Why can I sign in to the Azure portal but not the Azure classic portal?**</span></span>

<span data-ttu-id="d9614-121">**A:**  The Azure portal does not require a valid subscription, and the classic portal does require a valid subscription.</span><span class="sxs-lookup"><span data-stu-id="d9614-121">**A:**  The Azure portal does not require a valid subscription, and the classic portal does require a valid subscription.</span></span>  <span data-ttu-id="d9614-122">If you do not have a subscription, you can't sign in to the classic portal.</span><span class="sxs-lookup"><span data-stu-id="d9614-122">If you do not have a subscription, you can't sign in to the classic portal.</span></span>
- - -
<span data-ttu-id="d9614-123">**Q:  What are the differences between Subscription Administrator and Directory Administrator?**</span><span class="sxs-lookup"><span data-stu-id="d9614-123">**Q:  What are the differences between Subscription Administrator and Directory Administrator?**</span></span>

<span data-ttu-id="d9614-124">**A:** By default, you are assigned the Subscription Administrator role when you sign up for Azure.</span><span class="sxs-lookup"><span data-stu-id="d9614-124">**A:** By default, you are assigned the Subscription Administrator role when you sign up for Azure.</span></span> <span data-ttu-id="d9614-125">A subscription admin can use either a Microsoft account or a work or school account from the directory that the Azure subscription is associated with.</span><span class="sxs-lookup"><span data-stu-id="d9614-125">A subscription admin can use either a Microsoft account or a work or school account from the directory that the Azure subscription is associated with.</span></span>  <span data-ttu-id="d9614-126">This role is authorized to manage services in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d9614-126">This role is authorized to manage services in the Azure portal.</span></span>

<span data-ttu-id="d9614-127">If others need to sign in and access services by using the same subscription, you can add them as co-admins.</span><span class="sxs-lookup"><span data-stu-id="d9614-127">If others need to sign in and access services by using the same subscription, you can add them as co-admins.</span></span> <span data-ttu-id="d9614-128">This role has the same access privileges as the service admin, but can’t change the association of subscriptions to Azure directories.</span><span class="sxs-lookup"><span data-stu-id="d9614-128">This role has the same access privileges as the service admin, but can’t change the association of subscriptions to Azure directories.</span></span>  <span data-ttu-id="d9614-129">For additional information on subscription admins, see [How to add or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) and [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="d9614-129">For additional information on subscription admins, see [How to add or change Azure administrator roles](../billing-add-change-azure-subscription-administrator.md) and [How Azure subscriptions are associated with Azure Active Directory](active-directory-how-subscriptions-associated-directory.md).</span></span>


<span data-ttu-id="d9614-130">Azure AD has a different set of admin roles to manage the directory and identity-related features.</span><span class="sxs-lookup"><span data-stu-id="d9614-130">Azure AD has a different set of admin roles to manage the directory and identity-related features.</span></span>  <span data-ttu-id="d9614-131">These admins will have access to various features in the Azure portal or the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="d9614-131">These admins will have access to various features in the Azure portal or the Azure classic portal.</span></span> <span data-ttu-id="d9614-132">The admin's role determines what they can do, like create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, or manage domains.</span><span class="sxs-lookup"><span data-stu-id="d9614-132">The admin's role determines what they can do, like create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, or manage domains.</span></span>  <span data-ttu-id="d9614-133">For additional information on Azure AD directory admins and their roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d9614-133">For additional information on Azure AD directory admins and their roles, see [Assigning administrator roles in Azure Active Directory](active-directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="d9614-134">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span><span class="sxs-lookup"><span data-stu-id="d9614-134">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span></span>

- - -
<span data-ttu-id="d9614-135">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span><span class="sxs-lookup"><span data-stu-id="d9614-135">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span></span>

<span data-ttu-id="d9614-136">**A:** No.</span><span class="sxs-lookup"><span data-stu-id="d9614-136">**A:** No.</span></span>  <span data-ttu-id="d9614-137">This is not currently available.</span><span class="sxs-lookup"><span data-stu-id="d9614-137">This is not currently available.</span></span>

- - -

## <a name="get-started-with-hybrid-azure-ad"></a><span data-ttu-id="d9614-138">Get started with Hybrid Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9614-138">Get started with Hybrid Azure AD</span></span>


<span data-ttu-id="d9614-139">**Q: How do I leave a tenant when I am added as a collaborator?**</span><span class="sxs-lookup"><span data-stu-id="d9614-139">**Q: How do I leave a tenant when I am added as a collaborator?**</span></span>

<span data-ttu-id="d9614-140">**A:** When you are added to another organization's tenant as a collaborator, you can use the "tenant switcher" in the upper right to switch between tenants.</span><span class="sxs-lookup"><span data-stu-id="d9614-140">**A:** When you are added to another organization's tenant as a collaborator, you can use the "tenant switcher" in the upper right to switch between tenants.</span></span>  <span data-ttu-id="d9614-141">Currently, there is no way to leave the inviting organization, and Microsoft is working on providing this functionality.</span><span class="sxs-lookup"><span data-stu-id="d9614-141">Currently, there is no way to leave the inviting organization, and Microsoft is working on providing this functionality.</span></span>  <span data-ttu-id="d9614-142">Until this feature is available, you can ask the inviting organization to remove you from their tenant.</span><span class="sxs-lookup"><span data-stu-id="d9614-142">Until this feature is available, you can ask the inviting organization to remove you from their tenant.</span></span>
- - -
<span data-ttu-id="d9614-143">**Q: How can I connect my on-premises directory to Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="d9614-143">**Q: How can I connect my on-premises directory to Azure AD?**</span></span>

<span data-ttu-id="d9614-144">**A:** You can connect your on-premises directory to Azure AD by using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d9614-144">**A:** You can connect your on-premises directory to Azure AD by using Azure AD Connect.</span></span>

<span data-ttu-id="d9614-145">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="d9614-145">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="d9614-146">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span><span class="sxs-lookup"><span data-stu-id="d9614-146">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span></span>

<span data-ttu-id="d9614-147">**A:** You only need to set up single sign-on (SSO) between your on-premises directory and Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9614-147">**A:** You only need to set up single sign-on (SSO) between your on-premises directory and Azure AD.</span></span> <span data-ttu-id="d9614-148">As long as you access your cloud applications through Azure AD, the service automatically drives your users to correctly authenticate with their on-premises credentials.</span><span class="sxs-lookup"><span data-stu-id="d9614-148">As long as you access your cloud applications through Azure AD, the service automatically drives your users to correctly authenticate with their on-premises credentials.</span></span>

<span data-ttu-id="d9614-149">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using the Azure AD Connect configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="d9614-149">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using the Azure AD Connect configuration wizard.</span></span>

<span data-ttu-id="d9614-150">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="d9614-150">For more information, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="d9614-151">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span><span class="sxs-lookup"><span data-stu-id="d9614-151">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span></span>

<span data-ttu-id="d9614-152">**A:** Yes, Azure AD provides you with the [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span><span class="sxs-lookup"><span data-stu-id="d9614-152">**A:** Yes, Azure AD provides you with the [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span></span> <span data-ttu-id="d9614-153">If you are an Office 365 customer, you can find many of the same capabilities in the Office 365 portal.</span><span class="sxs-lookup"><span data-stu-id="d9614-153">If you are an Office 365 customer, you can find many of the same capabilities in the Office 365 portal.</span></span>

<span data-ttu-id="d9614-154">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d9614-154">For more information, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

- - -
<span data-ttu-id="d9614-155">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span><span class="sxs-lookup"><span data-stu-id="d9614-155">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span></span>

<span data-ttu-id="d9614-156">**A:** Yes.</span><span class="sxs-lookup"><span data-stu-id="d9614-156">**A:** Yes.</span></span> <span data-ttu-id="d9614-157">The Azure AD Premium edition provides you with Azure AD Connect Health.</span><span class="sxs-lookup"><span data-stu-id="d9614-157">The Azure AD Premium edition provides you with Azure AD Connect Health.</span></span> <span data-ttu-id="d9614-158">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and the synchronization services.</span><span class="sxs-lookup"><span data-stu-id="d9614-158">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and the synchronization services.</span></span>  

<span data-ttu-id="d9614-159">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in the cloud](active-directory-aadconnect-health.md).</span><span class="sxs-lookup"><span data-stu-id="d9614-159">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in the cloud](active-directory-aadconnect-health.md).</span></span>  

- - -
## <a name="password-management"></a><span data-ttu-id="d9614-160">Password management</span><span class="sxs-lookup"><span data-stu-id="d9614-160">Password management</span></span>
<span data-ttu-id="d9614-161">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible to use Azure AD self-service password reset (SSPR) with password write-back and not store passwords in the cloud?)**</span><span class="sxs-lookup"><span data-stu-id="d9614-161">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible to use Azure AD self-service password reset (SSPR) with password write-back and not store passwords in the cloud?)**</span></span>

<span data-ttu-id="d9614-162">**A:** You do not need to synchronize your Active Directory passwords to Azure AD to enable write-back.</span><span class="sxs-lookup"><span data-stu-id="d9614-162">**A:** You do not need to synchronize your Active Directory passwords to Azure AD to enable write-back.</span></span> <span data-ttu-id="d9614-163">In a federated environment, Azure AD single sign-on (SSO) relies on the on-premises directory to authenticate the user.</span><span class="sxs-lookup"><span data-stu-id="d9614-163">In a federated environment, Azure AD single sign-on (SSO) relies on the on-premises directory to authenticate the user.</span></span> <span data-ttu-id="d9614-164">This scenario does not require the on-premises password to be tracked in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9614-164">This scenario does not require the on-premises password to be tracked in Azure AD.</span></span>

- - -
<span data-ttu-id="d9614-165">**Q: How long does it take for a password to be written back to Active Directory on-premises?**</span><span class="sxs-lookup"><span data-stu-id="d9614-165">**Q: How long does it take for a password to be written back to Active Directory on-premises?**</span></span>

<span data-ttu-id="d9614-166">**A:** Password write-back operates in real time.</span><span class="sxs-lookup"><span data-stu-id="d9614-166">**A:** Password write-back operates in real time.</span></span>

<span data-ttu-id="d9614-167">For more information, see [Getting started with password management](active-directory-passwords-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="d9614-167">For more information, see [Getting started with password management](active-directory-passwords-getting-started.md).</span></span>

- - -
<span data-ttu-id="d9614-168">**Q: Can I use password write-back with passwords that are managed by an admin?**</span><span class="sxs-lookup"><span data-stu-id="d9614-168">**Q: Can I use password write-back with passwords that are managed by an admin?**</span></span>

<span data-ttu-id="d9614-169">**A:** Yes, if you have password write-back enabled, the password operations performed by an admin are written back to your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="d9614-169">**A:** Yes, if you have password write-back enabled, the password operations performed by an admin are written back to your on-premises environment.</span></span>  

<span data-ttu-id="d9614-170">For more answers to password-related questions, see [Password management frequently asked questions](active-directory-passwords-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d9614-170">For more answers to password-related questions, see [Password management frequently asked questions](active-directory-passwords-faq.md).</span></span>
- - -
<span data-ttu-id="d9614-171">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying to change my password?**</span><span class="sxs-lookup"><span data-stu-id="d9614-171">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying to change my password?**</span></span>

<span data-ttu-id="d9614-172">**A:** For this type of situation, there are a couple of options.</span><span class="sxs-lookup"><span data-stu-id="d9614-172">**A:** For this type of situation, there are a couple of options.</span></span>  <span data-ttu-id="d9614-173">Use self-service password reset (SSPR) if it's available.</span><span class="sxs-lookup"><span data-stu-id="d9614-173">Use self-service password reset (SSPR) if it's available.</span></span>  <span data-ttu-id="d9614-174">Whether SSPR works depends on how it's configured.</span><span class="sxs-lookup"><span data-stu-id="d9614-174">Whether SSPR works depends on how it's configured.</span></span>  <span data-ttu-id="d9614-175">For more information, see [How does the password reset portal work](active-directory-passwords-learn-more.md#how-does-the-password-reset-portal-work).</span><span class="sxs-lookup"><span data-stu-id="d9614-175">For more information, see [How does the password reset portal work](active-directory-passwords-learn-more.md#how-does-the-password-reset-portal-work).</span></span>

<span data-ttu-id="d9614-176">For Office 365 users, your admin can reset the password by using the steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="d9614-176">For Office 365 users, your admin can reset the password by using the steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span></span>

<span data-ttu-id="d9614-177">For Azure AD accounts, admins can reset passwords by using one of the following:</span><span class="sxs-lookup"><span data-stu-id="d9614-177">For Azure AD accounts, admins can reset passwords by using one of the following:</span></span>

- [<span data-ttu-id="d9614-178">Reset accounts in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d9614-178">Reset accounts in the Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
- [<span data-ttu-id="d9614-179">Reset accounts in the classic portal</span><span class="sxs-lookup"><span data-stu-id="d9614-179">Reset accounts in the classic portal</span></span>](active-directory-create-users-reset-password.md)
- [<span data-ttu-id="d9614-180">Using PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9614-180">Using PowerShell</span></span>](https://docs.microsoft.com/en-us/powershell/msonline/v1/Set-MsolUserPassword?redirectedfrom=msdn)


- - -
## <a name="security"></a><span data-ttu-id="d9614-181">Security</span><span class="sxs-lookup"><span data-stu-id="d9614-181">Security</span></span>
<span data-ttu-id="d9614-182">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span><span class="sxs-lookup"><span data-stu-id="d9614-182">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span></span></br>
<span data-ttu-id="d9614-183">We use a more sophisticated strategy to lock accounts.</span><span class="sxs-lookup"><span data-stu-id="d9614-183">We use a more sophisticated strategy to lock accounts.</span></span>  <span data-ttu-id="d9614-184">This is based on the IP of the request and the passwords entered.</span><span class="sxs-lookup"><span data-stu-id="d9614-184">This is based on the IP of the request and the passwords entered.</span></span> <span data-ttu-id="d9614-185">The duration of the lockout also increases based on the likelihood that it is an attack.</span><span class="sxs-lookup"><span data-stu-id="d9614-185">The duration of the lockout also increases based on the likelihood that it is an attack.</span></span>  

<span data-ttu-id="d9614-186">**Q:  Certain (common) passwords get rejected with the messages ‘this password has been used to many times’, does this refer to passwords used in the current active directory?**</span><span class="sxs-lookup"><span data-stu-id="d9614-186">**Q:  Certain (common) passwords get rejected with the messages ‘this password has been used to many times’, does this refer to passwords used in the current active directory?**</span></span></br>
<span data-ttu-id="d9614-187">This refers to passwords that are globally common, such as any variants of “Password” and “123456”.</span><span class="sxs-lookup"><span data-stu-id="d9614-187">This refers to passwords that are globally common, such as any variants of “Password” and “123456”.</span></span>

<span data-ttu-id="d9614-188">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span><span class="sxs-lookup"><span data-stu-id="d9614-188">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span></span></br>
<span data-ttu-id="d9614-189">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span><span class="sxs-lookup"><span data-stu-id="d9614-189">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span></span> 

## <a name="application-access"></a><span data-ttu-id="d9614-190">Application access</span><span class="sxs-lookup"><span data-stu-id="d9614-190">Application access</span></span>
<span data-ttu-id="d9614-191">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span><span class="sxs-lookup"><span data-stu-id="d9614-191">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span></span>

<span data-ttu-id="d9614-192">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span><span class="sxs-lookup"><span data-stu-id="d9614-192">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span></span> <span data-ttu-id="d9614-193">All pre-integrated applications support single sign-on (SSO).</span><span class="sxs-lookup"><span data-stu-id="d9614-193">All pre-integrated applications support single sign-on (SSO).</span></span> <span data-ttu-id="d9614-194">SSO lets you use your organizational credentials to access your apps.</span><span class="sxs-lookup"><span data-stu-id="d9614-194">SSO lets you use your organizational credentials to access your apps.</span></span> <span data-ttu-id="d9614-195">Some of the applications also support automated provisioning and de-provisioning.</span><span class="sxs-lookup"><span data-stu-id="d9614-195">Some of the applications also support automated provisioning and de-provisioning.</span></span>

<span data-ttu-id="d9614-196">For a complete list of the pre-integrated applications, see the [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="d9614-196">For a complete list of the pre-integrated applications, see the [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span></span>

- - -
<span data-ttu-id="d9614-197">**Q: What if the application I need is not in the Azure AD marketplace?**</span><span class="sxs-lookup"><span data-stu-id="d9614-197">**Q: What if the application I need is not in the Azure AD marketplace?**</span></span>

<span data-ttu-id="d9614-198">**A:** With Azure AD Premium, you can add and configure any application that you want.</span><span class="sxs-lookup"><span data-stu-id="d9614-198">**A:** With Azure AD Premium, you can add and configure any application that you want.</span></span> <span data-ttu-id="d9614-199">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span><span class="sxs-lookup"><span data-stu-id="d9614-199">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span></span>  

<span data-ttu-id="d9614-200">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="d9614-200">For more information, see:</span></span>

* [<span data-ttu-id="d9614-201">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span><span class="sxs-lookup"><span data-stu-id="d9614-201">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](active-directory-saas-custom-apps.md)
* [<span data-ttu-id="d9614-202">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span><span class="sxs-lookup"><span data-stu-id="d9614-202">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)

- - -
<span data-ttu-id="d9614-203">**Q: How do users sign in to applications by using Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="d9614-203">**Q: How do users sign in to applications by using Azure AD?**</span></span>

<span data-ttu-id="d9614-204">**A:** Azure AD provides several ways for users to view and access their applications, such as:</span><span class="sxs-lookup"><span data-stu-id="d9614-204">**A:** Azure AD provides several ways for users to view and access their applications, such as:</span></span>

* <span data-ttu-id="d9614-205">The Azure AD access panel</span><span class="sxs-lookup"><span data-stu-id="d9614-205">The Azure AD access panel</span></span>
* <span data-ttu-id="d9614-206">The Office 365 application launcher</span><span class="sxs-lookup"><span data-stu-id="d9614-206">The Office 365 application launcher</span></span>
* <span data-ttu-id="d9614-207">Direct sign-in to federated apps</span><span class="sxs-lookup"><span data-stu-id="d9614-207">Direct sign-in to federated apps</span></span>
* <span data-ttu-id="d9614-208">Deep links to federated, password-based, or existing apps</span><span class="sxs-lookup"><span data-stu-id="d9614-208">Deep links to federated, password-based, or existing apps</span></span>

<span data-ttu-id="d9614-209">For more information, see [Deploying Azure AD integrated applications to users](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="d9614-209">For more information, see [Deploying Azure AD integrated applications to users](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

- - -
<span data-ttu-id="d9614-210">**Q: What are the different ways Azure AD enables authentication and single sign-on to applications?**</span><span class="sxs-lookup"><span data-stu-id="d9614-210">**Q: What are the different ways Azure AD enables authentication and single sign-on to applications?**</span></span>

<span data-ttu-id="d9614-211">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="d9614-211">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span></span> <span data-ttu-id="d9614-212">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span><span class="sxs-lookup"><span data-stu-id="d9614-212">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span></span>  

<span data-ttu-id="d9614-213">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="d9614-213">For more information, see:</span></span>

* [<span data-ttu-id="d9614-214">Authentication Scenarios for Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9614-214">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)
* [<span data-ttu-id="d9614-215">Active Directory authentication protocols</span><span class="sxs-lookup"><span data-stu-id="d9614-215">Active Directory authentication protocols</span></span>](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [<span data-ttu-id="d9614-216">How does single sign-on with Azure Active Directory work?</span><span class="sxs-lookup"><span data-stu-id="d9614-216">How does single sign-on with Azure Active Directory work?</span></span>](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
<span data-ttu-id="d9614-217">**Q: Can I add applications I’m running on-premises?**</span><span class="sxs-lookup"><span data-stu-id="d9614-217">**Q: Can I add applications I’m running on-premises?**</span></span>

<span data-ttu-id="d9614-218">**A:** Azure AD Application Proxy provides you with easy and secure access to on-premises web applications that you choose.</span><span class="sxs-lookup"><span data-stu-id="d9614-218">**A:** Azure AD Application Proxy provides you with easy and secure access to on-premises web applications that you choose.</span></span> <span data-ttu-id="d9614-219">You can access these applications in the same way that you access your software as a service (SaaS) apps in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9614-219">You can access these applications in the same way that you access your software as a service (SaaS) apps in Azure AD.</span></span> <span data-ttu-id="d9614-220">There is no need for a VPN or to change your network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="d9614-220">There is no need for a VPN or to change your network infrastructure.</span></span>  

<span data-ttu-id="d9614-221">For more information, see [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d9614-221">For more information, see [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>

- - -
<span data-ttu-id="d9614-222">**Q: How do I require multi-factor authentication for users who access a particular application?**</span><span class="sxs-lookup"><span data-stu-id="d9614-222">**Q: How do I require multi-factor authentication for users who access a particular application?**</span></span>

<span data-ttu-id="d9614-223">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span><span class="sxs-lookup"><span data-stu-id="d9614-223">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span></span> <span data-ttu-id="d9614-224">In your policy, you can require multi-factor authentication always, or when users are not connected to the local network.</span><span class="sxs-lookup"><span data-stu-id="d9614-224">In your policy, you can require multi-factor authentication always, or when users are not connected to the local network.</span></span>  

<span data-ttu-id="d9614-225">For more information, see [Securing access to Office 365 and other apps connected to Azure Active Directory](active-directory-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="d9614-225">For more information, see [Securing access to Office 365 and other apps connected to Azure Active Directory](active-directory-conditional-access.md).</span></span>

- - -
<span data-ttu-id="d9614-226">**Q: What is automated user provisioning for SaaS apps?**</span><span class="sxs-lookup"><span data-stu-id="d9614-226">**Q: What is automated user provisioning for SaaS apps?**</span></span>

<span data-ttu-id="d9614-227">**A:** Use Azure AD to automate the creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="d9614-227">**A:** Use Azure AD to automate the creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span></span>

<span data-ttu-id="d9614-228">For more information, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](active-directory-saas-app-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="d9614-228">For more information, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](active-directory-saas-app-provisioning.md).</span></span>

- - -
<span data-ttu-id="d9614-229">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="d9614-229">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span></span>

<span data-ttu-id="d9614-230">**A:**  No.</span><span class="sxs-lookup"><span data-stu-id="d9614-230">**A:**  No.</span></span>  <span data-ttu-id="d9614-231">Azure AD does not support the LDAP protocol.</span><span class="sxs-lookup"><span data-stu-id="d9614-231">Azure AD does not support the LDAP protocol.</span></span>
