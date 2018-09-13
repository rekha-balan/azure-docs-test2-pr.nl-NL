---
title: Azure AD FAQ | Microsoft Docs
description: Azure Active Directory FAQ answers common questions about Azure and Azure Active Directory, password management, and application access.
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
editor: ''
ms.assetid: b8207760-9714-4871-93d5-f9893de31c8f
ms.service: active-directory
ms.component: fundamentals
ms.workload: identity
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/14/2017
ms.author: lizross
ms.openlocfilehash: cc9b5810085d3300861735a95a94e577bf61d70e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870950"
---
# <a name="azure-active-directory-faq"></a><span data-ttu-id="5020d-103">Azure Active Directory FAQ</span><span class="sxs-lookup"><span data-stu-id="5020d-103">Azure Active Directory FAQ</span></span>
<span data-ttu-id="5020d-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span><span class="sxs-lookup"><span data-stu-id="5020d-104">Azure Active Directory (Azure AD) is a comprehensive identity as a service (IDaaS) solution that spans all aspects of identity, access management, and security.</span></span>

<span data-ttu-id="5020d-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-105">For more information, see [What is Azure Active Directory?](active-directory-whatis.md).</span></span>


## <a name="access-azure-and-azure-active-directory"></a><span data-ttu-id="5020d-106">Access Azure and Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5020d-106">Access Azure and Azure Active Directory</span></span>
<span data-ttu-id="5020d-107">**Q: Why do I get “No subscriptions found” when I try to access Azure AD in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="5020d-107">**Q: Why do I get “No subscriptions found” when I try to access Azure AD in the Azure portal?**</span></span>

<span data-ttu-id="5020d-108">**A:** To access the Azure portal, each user needs permissions with an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5020d-108">**A:** To access the Azure portal, each user needs permissions with an Azure subscription.</span></span> <span data-ttu-id="5020d-109">If you have a paid Office 365 or Azure AD subscription, go to [https://aka.ms/accessAAD](https://aka.ms/accessAAD) for a one-time activation step.</span><span class="sxs-lookup"><span data-stu-id="5020d-109">If you have a paid Office 365 or Azure AD subscription, go to [https://aka.ms/accessAAD](https://aka.ms/accessAAD) for a one-time activation step.</span></span> <span data-ttu-id="5020d-110">Otherwise, you will need to activate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span><span class="sxs-lookup"><span data-stu-id="5020d-110">Otherwise, you will need to activate a free [Azure account](https://azure.microsoft.com/pricing/free-trial/) or a paid subscription.</span></span>

<span data-ttu-id="5020d-111">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="5020d-111">For more information, see:</span></span>

* [<span data-ttu-id="5020d-112">How Azure subscriptions are associated with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5020d-112">How Azure subscriptions are associated with Azure Active Directory</span></span>](active-directory-how-subscriptions-associated-directory.md)

- - -
<span data-ttu-id="5020d-113">**Q: What’s the relationship between Azure AD, Office 365, and Azure?**</span><span class="sxs-lookup"><span data-stu-id="5020d-113">**Q: What’s the relationship between Azure AD, Office 365, and Azure?**</span></span>

<span data-ttu-id="5020d-114">**A:** Azure AD provides you with common identity and access capabilities to all web services.</span><span class="sxs-lookup"><span data-stu-id="5020d-114">**A:** Azure AD provides you with common identity and access capabilities to all web services.</span></span> <span data-ttu-id="5020d-115">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD to help turn on sign-on and access management for all these services.</span><span class="sxs-lookup"><span data-stu-id="5020d-115">Whether you are using Office 365, Microsoft Azure, Intune, or others, you're already using Azure AD to help turn on sign-on and access management for all these services.</span></span>

<span data-ttu-id="5020d-116">All users who are set up to use web services are defined as user accounts in one or more Azure AD instances.</span><span class="sxs-lookup"><span data-stu-id="5020d-116">All users who are set up to use web services are defined as user accounts in one or more Azure AD instances.</span></span> <span data-ttu-id="5020d-117">You can set up these accounts for free Azure AD capabilities like cloud application access.</span><span class="sxs-lookup"><span data-stu-id="5020d-117">You can set up these accounts for free Azure AD capabilities like cloud application access.</span></span>

<span data-ttu-id="5020d-118">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span><span class="sxs-lookup"><span data-stu-id="5020d-118">Azure AD paid services like Enterprise Mobility + Security complement other web services like Office 365 and Microsoft Azure with comprehensive enterprise-scale management and security solutions.</span></span>

- - -

<span data-ttu-id="5020d-119">**Q:  What are the differences between Owner and Global Administrator?**</span><span class="sxs-lookup"><span data-stu-id="5020d-119">**Q:  What are the differences between Owner and Global Administrator?**</span></span>

<span data-ttu-id="5020d-120">**A:** By default, the person who signs up for an Azure subscription is assigned the Owner role for Azure resources.</span><span class="sxs-lookup"><span data-stu-id="5020d-120">**A:** By default, the person who signs up for an Azure subscription is assigned the Owner role for Azure resources.</span></span> <span data-ttu-id="5020d-121">An Owner can use either a Microsoft account or a work or school account from the directory that the Azure subscription is associated with.</span><span class="sxs-lookup"><span data-stu-id="5020d-121">An Owner can use either a Microsoft account or a work or school account from the directory that the Azure subscription is associated with.</span></span>  <span data-ttu-id="5020d-122">This role is authorized to manage services in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5020d-122">This role is authorized to manage services in the Azure portal.</span></span>

<span data-ttu-id="5020d-123">If others need to sign in and access services by using the same subscription, you can assign them the appropriate [built-in role](../../role-based-access-control/built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-123">If others need to sign in and access services by using the same subscription, you can assign them the appropriate [built-in role](../../role-based-access-control/built-in-roles.md).</span></span> <span data-ttu-id="5020d-124">For additional information, see [Manage access using RBAC and the Azure portal](../../role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-124">For additional information, see [Manage access using RBAC and the Azure portal](../../role-based-access-control/role-assignments-portal.md).</span></span>

<span data-ttu-id="5020d-125">By default, the person who signs up for an Azure subscription is assigned the Global Administrator role for the directory.</span><span class="sxs-lookup"><span data-stu-id="5020d-125">By default, the person who signs up for an Azure subscription is assigned the Global Administrator role for the directory.</span></span> <span data-ttu-id="5020d-126">The Global Administrator has access to all Azure AD directory features.</span><span class="sxs-lookup"><span data-stu-id="5020d-126">The Global Administrator has access to all Azure AD directory features.</span></span> <span data-ttu-id="5020d-127">Azure AD has a different set of administrator roles to manage the directory and identity-related features.</span><span class="sxs-lookup"><span data-stu-id="5020d-127">Azure AD has a different set of administrator roles to manage the directory and identity-related features.</span></span> <span data-ttu-id="5020d-128">These administrators will have access to various features in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5020d-128">These administrators will have access to various features in the Azure portal.</span></span> <span data-ttu-id="5020d-129">The administrator's role determines what they can do, like create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, or manage domains.</span><span class="sxs-lookup"><span data-stu-id="5020d-129">The administrator's role determines what they can do, like create or edit users, assign administrative roles to others, reset user passwords, manage user licenses, or manage domains.</span></span>  <span data-ttu-id="5020d-130">For additional information on Azure AD directory admins and their roles, see [Assign a user to administrator roles in Azure Active Directory](active-directory-users-assign-role-azure-portal.md) and [Assigning administrator roles in Azure Active Directory](../users-groups-roles/directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-130">For additional information on Azure AD directory admins and their roles, see [Assign a user to administrator roles in Azure Active Directory](active-directory-users-assign-role-azure-portal.md) and [Assigning administrator roles in Azure Active Directory](../users-groups-roles/directory-assign-admin-roles.md).</span></span>

<span data-ttu-id="5020d-131">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span><span class="sxs-lookup"><span data-stu-id="5020d-131">Additionally, Azure AD paid services like Enterprise Mobility + Security complement other web services, such as Office 365 and Microsoft Azure, with comprehensive enterprise-scale management and security solutions.</span></span>

- - -
<span data-ttu-id="5020d-132">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span><span class="sxs-lookup"><span data-stu-id="5020d-132">**Q: Is there a report that shows when my Azure AD user licenses will expire?**</span></span>

<span data-ttu-id="5020d-133">**A:** No.</span><span class="sxs-lookup"><span data-stu-id="5020d-133">**A:** No.</span></span>  <span data-ttu-id="5020d-134">This is not currently available.</span><span class="sxs-lookup"><span data-stu-id="5020d-134">This is not currently available.</span></span>

- - -

## <a name="get-started-with-hybrid-azure-ad"></a><span data-ttu-id="5020d-135">Get started with Hybrid Azure AD</span><span class="sxs-lookup"><span data-stu-id="5020d-135">Get started with Hybrid Azure AD</span></span>


<span data-ttu-id="5020d-136">**Q: How do I leave a tenant when I am added as a collaborator?**</span><span class="sxs-lookup"><span data-stu-id="5020d-136">**Q: How do I leave a tenant when I am added as a collaborator?**</span></span>

<span data-ttu-id="5020d-137">**A:** When you are added to another organization's tenant as a collaborator, you can use the "tenant switcher" in the upper right to switch between tenants.</span><span class="sxs-lookup"><span data-stu-id="5020d-137">**A:** When you are added to another organization's tenant as a collaborator, you can use the "tenant switcher" in the upper right to switch between tenants.</span></span>  <span data-ttu-id="5020d-138">Currently, there is no way to leave the inviting organization, and Microsoft is working on providing this functionality.</span><span class="sxs-lookup"><span data-stu-id="5020d-138">Currently, there is no way to leave the inviting organization, and Microsoft is working on providing this functionality.</span></span>  <span data-ttu-id="5020d-139">Until this feature is available, you can ask the inviting organization to remove you from their tenant.</span><span class="sxs-lookup"><span data-stu-id="5020d-139">Until this feature is available, you can ask the inviting organization to remove you from their tenant.</span></span>
- - -
<span data-ttu-id="5020d-140">**Q: How can I connect my on-premises directory to Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="5020d-140">**Q: How can I connect my on-premises directory to Azure AD?**</span></span>

<span data-ttu-id="5020d-141">**A:** You can connect your on-premises directory to Azure AD by using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="5020d-141">**A:** You can connect your on-premises directory to Azure AD by using Azure AD Connect.</span></span>

<span data-ttu-id="5020d-142">For more information, see [Integrating your on-premises identities with Azure Active Directory](../connect/active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-142">For more information, see [Integrating your on-premises identities with Azure Active Directory](../connect/active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="5020d-143">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span><span class="sxs-lookup"><span data-stu-id="5020d-143">**Q: How do I set up SSO between my on-premises directory and my cloud applications?**</span></span>

<span data-ttu-id="5020d-144">**A:** You only need to set up single sign-on (SSO) between your on-premises directory and Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5020d-144">**A:** You only need to set up single sign-on (SSO) between your on-premises directory and Azure AD.</span></span> <span data-ttu-id="5020d-145">As long as you access your cloud applications through Azure AD, the service automatically drives your users to correctly authenticate with their on-premises credentials.</span><span class="sxs-lookup"><span data-stu-id="5020d-145">As long as you access your cloud applications through Azure AD, the service automatically drives your users to correctly authenticate with their on-premises credentials.</span></span>

<span data-ttu-id="5020d-146">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using the Azure AD Connect configuration wizard.</span><span class="sxs-lookup"><span data-stu-id="5020d-146">Implementing SSO from on-premises can be easily achieved with federation solutions such as Active Directory Federation Services (AD FS), or by configuring password hash sync. You can easily deploy both options by using the Azure AD Connect configuration wizard.</span></span>

<span data-ttu-id="5020d-147">For more information, see [Integrating your on-premises identities with Azure Active Directory](../connect/active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-147">For more information, see [Integrating your on-premises identities with Azure Active Directory](../connect/active-directory-aadconnect.md).</span></span>

- - -
<span data-ttu-id="5020d-148">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span><span class="sxs-lookup"><span data-stu-id="5020d-148">**Q: Does Azure AD provide a self-service portal for users in my organization?**</span></span>

<span data-ttu-id="5020d-149">**A:** Yes, Azure AD provides you with the [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span><span class="sxs-lookup"><span data-stu-id="5020d-149">**A:** Yes, Azure AD provides you with the [Azure AD Access Panel](http://myapps.microsoft.com) for user self-service and application access.</span></span> <span data-ttu-id="5020d-150">If you are an Office 365 customer, you can find many of the same capabilities in the Office 365 portal.</span><span class="sxs-lookup"><span data-stu-id="5020d-150">If you are an Office 365 customer, you can find many of the same capabilities in the Office 365 portal.</span></span>

<span data-ttu-id="5020d-151">For more information, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-151">For more information, see [Introduction to the Access Panel](../user-help/active-directory-saas-access-panel-introduction.md).</span></span>

- - -
<span data-ttu-id="5020d-152">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span><span class="sxs-lookup"><span data-stu-id="5020d-152">**Q: Does Azure AD help me manage my on-premises infrastructure?**</span></span>

<span data-ttu-id="5020d-153">**A:** Yes.</span><span class="sxs-lookup"><span data-stu-id="5020d-153">**A:** Yes.</span></span> <span data-ttu-id="5020d-154">The Azure AD Premium edition provides you with Azure AD Connect Health.</span><span class="sxs-lookup"><span data-stu-id="5020d-154">The Azure AD Premium edition provides you with Azure AD Connect Health.</span></span> <span data-ttu-id="5020d-155">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and the synchronization services.</span><span class="sxs-lookup"><span data-stu-id="5020d-155">Azure AD Connect Health helps you monitor and gain insight into your on-premises identity infrastructure and the synchronization services.</span></span>  

<span data-ttu-id="5020d-156">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in the cloud](../connect-health/active-directory-aadconnect-health.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-156">For more information, see [Monitor your on-premises identity infrastructure and synchronization services in the cloud](../connect-health/active-directory-aadconnect-health.md).</span></span>  

- - -
## <a name="password-management"></a><span data-ttu-id="5020d-157">Password management</span><span class="sxs-lookup"><span data-stu-id="5020d-157">Password management</span></span>
<span data-ttu-id="5020d-158">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible to use Azure AD self-service password reset (SSPR) with password write-back and not store passwords in the cloud?)**</span><span class="sxs-lookup"><span data-stu-id="5020d-158">**Q: Can I use Azure AD password write-back without password sync? (In this scenario, is it possible to use Azure AD self-service password reset (SSPR) with password write-back and not store passwords in the cloud?)**</span></span>

<span data-ttu-id="5020d-159">**A:** You do not need to synchronize your Active Directory passwords to Azure AD to enable write-back.</span><span class="sxs-lookup"><span data-stu-id="5020d-159">**A:** You do not need to synchronize your Active Directory passwords to Azure AD to enable write-back.</span></span> <span data-ttu-id="5020d-160">In a federated environment, Azure AD single sign-on (SSO) relies on the on-premises directory to authenticate the user.</span><span class="sxs-lookup"><span data-stu-id="5020d-160">In a federated environment, Azure AD single sign-on (SSO) relies on the on-premises directory to authenticate the user.</span></span> <span data-ttu-id="5020d-161">This scenario does not require the on-premises password to be tracked in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5020d-161">This scenario does not require the on-premises password to be tracked in Azure AD.</span></span>

- - -
<span data-ttu-id="5020d-162">**Q: How long does it take for a password to be written back to Active Directory on-premises?**</span><span class="sxs-lookup"><span data-stu-id="5020d-162">**Q: How long does it take for a password to be written back to Active Directory on-premises?**</span></span>

<span data-ttu-id="5020d-163">**A:** Password write-back operates in real time.</span><span class="sxs-lookup"><span data-stu-id="5020d-163">**A:** Password write-back operates in real time.</span></span>

<span data-ttu-id="5020d-164">For more information, see [Getting started with password management](../authentication/quickstart-sspr.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-164">For more information, see [Getting started with password management](../authentication/quickstart-sspr.md).</span></span>

- - -
<span data-ttu-id="5020d-165">**Q: Can I use password write-back with passwords that are managed by an admin?**</span><span class="sxs-lookup"><span data-stu-id="5020d-165">**Q: Can I use password write-back with passwords that are managed by an admin?**</span></span>

<span data-ttu-id="5020d-166">**A:** Yes, if you have password write-back enabled, the password operations performed by an admin are written back to your on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="5020d-166">**A:** Yes, if you have password write-back enabled, the password operations performed by an admin are written back to your on-premises environment.</span></span>  

<span data-ttu-id="5020d-167">For more answers to password-related questions, see [Password management frequently asked questions](../authentication/active-directory-passwords-faq.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-167">For more answers to password-related questions, see [Password management frequently asked questions](../authentication/active-directory-passwords-faq.md).</span></span>
- - -
<span data-ttu-id="5020d-168">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying to change my password?**</span><span class="sxs-lookup"><span data-stu-id="5020d-168">**Q:  What can I do if I can't remember my existing Office 365/Azure AD password while trying to change my password?**</span></span>

<span data-ttu-id="5020d-169">**A:** For this type of situation, there are a couple of options.</span><span class="sxs-lookup"><span data-stu-id="5020d-169">**A:** For this type of situation, there are a couple of options.</span></span>  <span data-ttu-id="5020d-170">Use self-service password reset (SSPR) if it's available.</span><span class="sxs-lookup"><span data-stu-id="5020d-170">Use self-service password reset (SSPR) if it's available.</span></span>  <span data-ttu-id="5020d-171">Whether SSPR works depends on how it's configured.</span><span class="sxs-lookup"><span data-stu-id="5020d-171">Whether SSPR works depends on how it's configured.</span></span>  <span data-ttu-id="5020d-172">For more information, see [How does the password reset portal work](../authentication/howto-sspr-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-172">For more information, see [How does the password reset portal work](../authentication/howto-sspr-deployment.md).</span></span>

<span data-ttu-id="5020d-173">For Office 365 users, your admin can reset the password by using the steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="5020d-173">For Office 365 users, your admin can reset the password by using the steps outlined in [Reset user passwords](https://support.office.com/en-us/article/Admins-Reset-user-passwords-7A5D073B-7FAE-4AA5-8F96-9ECD041ABA9C?ui=en-US&rs=en-US&ad=US).</span></span>

<span data-ttu-id="5020d-174">For Azure AD accounts, admins can reset passwords by using one of the following:</span><span class="sxs-lookup"><span data-stu-id="5020d-174">For Azure AD accounts, admins can reset passwords by using one of the following:</span></span>

- [<span data-ttu-id="5020d-175">Reset accounts in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="5020d-175">Reset accounts in the Azure portal</span></span>](active-directory-users-reset-password-azure-portal.md)
- [<span data-ttu-id="5020d-176">Using PowerShell</span><span class="sxs-lookup"><span data-stu-id="5020d-176">Using PowerShell</span></span>](/powershell/module/msonline/set-msoluserpassword?view=azureadps-1.0)


- - -
## <a name="security"></a><span data-ttu-id="5020d-177">Security</span><span class="sxs-lookup"><span data-stu-id="5020d-177">Security</span></span>
<span data-ttu-id="5020d-178">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span><span class="sxs-lookup"><span data-stu-id="5020d-178">**Q: Are accounts locked after a specific number of failed attempts or is there a more sophisticated strategy used?**</span></span>

<span data-ttu-id="5020d-179">We use a more sophisticated strategy to lock accounts.</span><span class="sxs-lookup"><span data-stu-id="5020d-179">We use a more sophisticated strategy to lock accounts.</span></span>  <span data-ttu-id="5020d-180">This is based on the IP of the request and the passwords entered.</span><span class="sxs-lookup"><span data-stu-id="5020d-180">This is based on the IP of the request and the passwords entered.</span></span> <span data-ttu-id="5020d-181">The duration of the lockout also increases based on the likelihood that it is an attack.</span><span class="sxs-lookup"><span data-stu-id="5020d-181">The duration of the lockout also increases based on the likelihood that it is an attack.</span></span>  

<span data-ttu-id="5020d-182">**Q:  Certain (common) passwords get rejected with the messages ‘this password has been used to many times’, does this refer to passwords used in the current active directory?**</span><span class="sxs-lookup"><span data-stu-id="5020d-182">**Q:  Certain (common) passwords get rejected with the messages ‘this password has been used to many times’, does this refer to passwords used in the current active directory?**</span></span>

<span data-ttu-id="5020d-183">This refers to passwords that are globally common, such as any variants of “Password” and “123456”.</span><span class="sxs-lookup"><span data-stu-id="5020d-183">This refers to passwords that are globally common, such as any variants of “Password” and “123456”.</span></span>

<span data-ttu-id="5020d-184">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span><span class="sxs-lookup"><span data-stu-id="5020d-184">**Q: Will a sign-in request from dubious sources (botnets, tor endpoint) be blocked in a B2C tenant or does this require a Basic or Premium edition tenant?**</span></span>

<span data-ttu-id="5020d-185">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span><span class="sxs-lookup"><span data-stu-id="5020d-185">We do have a gateway that filters requests and provides some protection from botnets, and is applied for all B2C tenants.</span></span>

## <a name="application-access"></a><span data-ttu-id="5020d-186">Application access</span><span class="sxs-lookup"><span data-stu-id="5020d-186">Application access</span></span>

<span data-ttu-id="5020d-187">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span><span class="sxs-lookup"><span data-stu-id="5020d-187">**Q: Where can I find a list of applications that are pre-integrated with Azure AD and their capabilities?**</span></span>

<span data-ttu-id="5020d-188">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span><span class="sxs-lookup"><span data-stu-id="5020d-188">**A:** Azure AD has more than 2,600 pre-integrated applications from Microsoft, application service providers, and partners.</span></span> <span data-ttu-id="5020d-189">All pre-integrated applications support single sign-on (SSO).</span><span class="sxs-lookup"><span data-stu-id="5020d-189">All pre-integrated applications support single sign-on (SSO).</span></span> <span data-ttu-id="5020d-190">SSO lets you use your organizational credentials to access your apps.</span><span class="sxs-lookup"><span data-stu-id="5020d-190">SSO lets you use your organizational credentials to access your apps.</span></span> <span data-ttu-id="5020d-191">Some of the applications also support automated provisioning and de-provisioning.</span><span class="sxs-lookup"><span data-stu-id="5020d-191">Some of the applications also support automated provisioning and de-provisioning.</span></span>

<span data-ttu-id="5020d-192">For a complete list of the pre-integrated applications, see the [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="5020d-192">For a complete list of the pre-integrated applications, see the [Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/).</span></span>

- - -
<span data-ttu-id="5020d-193">**Q: What if the application I need is not in the Azure AD marketplace?**</span><span class="sxs-lookup"><span data-stu-id="5020d-193">**Q: What if the application I need is not in the Azure AD marketplace?**</span></span>

<span data-ttu-id="5020d-194">**A:** With Azure AD Premium, you can add and configure any application that you want.</span><span class="sxs-lookup"><span data-stu-id="5020d-194">**A:** With Azure AD Premium, you can add and configure any application that you want.</span></span> <span data-ttu-id="5020d-195">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span><span class="sxs-lookup"><span data-stu-id="5020d-195">Depending on your application’s capabilities and your preferences, you can configure SSO and automated provisioning.</span></span>  

<span data-ttu-id="5020d-196">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="5020d-196">For more information, see:</span></span>

* [<span data-ttu-id="5020d-197">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span><span class="sxs-lookup"><span data-stu-id="5020d-197">Configuring single sign-on to applications that are not in the Azure Active Directory application gallery</span></span>](../manage-apps/configure-federated-single-sign-on-non-gallery-applications.md)
* [<span data-ttu-id="5020d-198">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span><span class="sxs-lookup"><span data-stu-id="5020d-198">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](../manage-apps/use-scim-to-provision-users-and-groups.md)

- - -
<span data-ttu-id="5020d-199">**Q: How do users sign in to applications by using Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="5020d-199">**Q: How do users sign in to applications by using Azure AD?**</span></span>

<span data-ttu-id="5020d-200">**A:** Azure AD provides several ways for users to view and access their applications, such as:</span><span class="sxs-lookup"><span data-stu-id="5020d-200">**A:** Azure AD provides several ways for users to view and access their applications, such as:</span></span>

* <span data-ttu-id="5020d-201">The Azure AD access panel</span><span class="sxs-lookup"><span data-stu-id="5020d-201">The Azure AD access panel</span></span>
* <span data-ttu-id="5020d-202">The Office 365 application launcher</span><span class="sxs-lookup"><span data-stu-id="5020d-202">The Office 365 application launcher</span></span>
* <span data-ttu-id="5020d-203">Direct sign-in to federated apps</span><span class="sxs-lookup"><span data-stu-id="5020d-203">Direct sign-in to federated apps</span></span>
* <span data-ttu-id="5020d-204">Deep links to federated, password-based, or existing apps</span><span class="sxs-lookup"><span data-stu-id="5020d-204">Deep links to federated, password-based, or existing apps</span></span>

<span data-ttu-id="5020d-205">For more information, see [Deploying Azure AD integrated applications to users](../manage-apps/what-is-single-sign-on.md#deploying-azure-ad-integrated-applications-to-users).</span><span class="sxs-lookup"><span data-stu-id="5020d-205">For more information, see [Deploying Azure AD integrated applications to users](../manage-apps/what-is-single-sign-on.md#deploying-azure-ad-integrated-applications-to-users).</span></span>

- - -
<span data-ttu-id="5020d-206">**Q: What are the different ways Azure AD enables authentication and single sign-on to applications?**</span><span class="sxs-lookup"><span data-stu-id="5020d-206">**Q: What are the different ways Azure AD enables authentication and single sign-on to applications?**</span></span>

<span data-ttu-id="5020d-207">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="5020d-207">**A:** Azure AD supports many standardized protocols for authentication and authorization, such as SAML 2.0, OpenID Connect, OAuth 2.0, and WS-Federation.</span></span> <span data-ttu-id="5020d-208">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span><span class="sxs-lookup"><span data-stu-id="5020d-208">Azure AD also supports password vaulting and automated sign-in capabilities for apps that only support forms-based authentication.</span></span>  

<span data-ttu-id="5020d-209">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="5020d-209">For more information, see:</span></span>

* [<span data-ttu-id="5020d-210">Authentication Scenarios for Azure AD</span><span class="sxs-lookup"><span data-stu-id="5020d-210">Authentication Scenarios for Azure AD</span></span>](../develop/authentication-scenarios.md)
* [<span data-ttu-id="5020d-211">Active Directory authentication protocols</span><span class="sxs-lookup"><span data-stu-id="5020d-211">Active Directory authentication protocols</span></span>](https://msdn.microsoft.com/library/azure/dn151124.aspx)
* [<span data-ttu-id="5020d-212">How does single sign-on with Azure Active Directory work?</span><span class="sxs-lookup"><span data-stu-id="5020d-212">How does single sign-on with Azure Active Directory work?</span></span>](../manage-apps/what-is-single-sign-on.md#how-does-single-sign-on-with-azure-active-directory-work)

- - -
<span data-ttu-id="5020d-213">**Q: Can I add applications I’m running on-premises?**</span><span class="sxs-lookup"><span data-stu-id="5020d-213">**Q: Can I add applications I’m running on-premises?**</span></span>

<span data-ttu-id="5020d-214">**A:** Azure AD Application Proxy provides you with easy and secure access to on-premises web applications that you choose.</span><span class="sxs-lookup"><span data-stu-id="5020d-214">**A:** Azure AD Application Proxy provides you with easy and secure access to on-premises web applications that you choose.</span></span> <span data-ttu-id="5020d-215">You can access these applications in the same way that you access your software as a service (SaaS) apps in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5020d-215">You can access these applications in the same way that you access your software as a service (SaaS) apps in Azure AD.</span></span> <span data-ttu-id="5020d-216">There is no need for a VPN or to change your network infrastructure.</span><span class="sxs-lookup"><span data-stu-id="5020d-216">There is no need for a VPN or to change your network infrastructure.</span></span>  

<span data-ttu-id="5020d-217">For more information, see [How to provide secure remote access to on-premises applications](../manage-apps/application-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-217">For more information, see [How to provide secure remote access to on-premises applications](../manage-apps/application-proxy.md).</span></span>

- - -
<span data-ttu-id="5020d-218">**Q: How do I require multi-factor authentication for users who access a particular application?**</span><span class="sxs-lookup"><span data-stu-id="5020d-218">**Q: How do I require multi-factor authentication for users who access a particular application?**</span></span>

<span data-ttu-id="5020d-219">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span><span class="sxs-lookup"><span data-stu-id="5020d-219">**A:** With Azure AD conditional access, you can assign a unique access policy for each application.</span></span> <span data-ttu-id="5020d-220">In your policy, you can require multi-factor authentication always, or when users are not connected to the local network.</span><span class="sxs-lookup"><span data-stu-id="5020d-220">In your policy, you can require multi-factor authentication always, or when users are not connected to the local network.</span></span>  

<span data-ttu-id="5020d-221">For more information, see [Securing access to Office 365 and other apps connected to Azure Active Directory](../active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-221">For more information, see [Securing access to Office 365 and other apps connected to Azure Active Directory](../active-directory-conditional-access-azure-portal.md).</span></span>

- - -
<span data-ttu-id="5020d-222">**Q: What is automated user provisioning for SaaS apps?**</span><span class="sxs-lookup"><span data-stu-id="5020d-222">**Q: What is automated user provisioning for SaaS apps?**</span></span>

<span data-ttu-id="5020d-223">**A:** Use Azure AD to automate the creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="5020d-223">**A:** Use Azure AD to automate the creation, maintenance, and removal of user identities in many popular cloud SaaS apps.</span></span>

<span data-ttu-id="5020d-224">For more information, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="5020d-224">For more information, see [Automate user provisioning and deprovisioning to SaaS applications with Azure Active Directory](../manage-apps/user-provisioning.md).</span></span>

- - -
<span data-ttu-id="5020d-225">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="5020d-225">**Q:  Can I set up a secure LDAP connection with Azure AD?**</span></span>

<span data-ttu-id="5020d-226">**A:**  No.</span><span class="sxs-lookup"><span data-stu-id="5020d-226">**A:**  No.</span></span> <span data-ttu-id="5020d-227">Azure AD does not support the LDAP protocol.</span><span class="sxs-lookup"><span data-stu-id="5020d-227">Azure AD does not support the LDAP protocol.</span></span> <span data-ttu-id="5020d-228">However, you can configure secure LDAP with Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="5020d-228">However, you can configure secure LDAP with Azure AD Domain Services.</span></span>
