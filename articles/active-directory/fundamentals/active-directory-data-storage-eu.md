---
title: Where Azure AD stores identity data for European customers | Microsoft Docs
description: Learn about where Microsoft Azure Active Directory stores identity-related data for its European customers.
services: active-directory
documentationcenter: ''
author: eross-msft
manager: mtillman
ms.author: lizross
ms.service: active-directory
ms.component: fundamentals
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: overview
ms.date: 05/17/2018
ms.custom: it-pro
ms.openlocfilehash: 0baa499f56fa6c074ac1c0f604e74f9e7adb5502
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865248"
---
# <a name="where-does-microsoft-azure-active-directory-azure-ad-store-identity-data-for-european-customers"></a><span data-ttu-id="4d205-103">Where does Microsoft Azure Active Directory (Azure AD) store identity data for European customers</span><span class="sxs-lookup"><span data-stu-id="4d205-103">Where does Microsoft Azure Active Directory (Azure AD) store identity data for European customers</span></span>
<span data-ttu-id="4d205-104">Azure AD helps you to manage user identities and to create intelligence-driven access policies that help secure your organization's resources.</span><span class="sxs-lookup"><span data-stu-id="4d205-104">Azure AD helps you to manage user identities and to create intelligence-driven access policies that help secure your organization's resources.</span></span> <span data-ttu-id="4d205-105">Identity data is stored in a location that's based on the address your organization provided when you subscribed to the service.</span><span class="sxs-lookup"><span data-stu-id="4d205-105">Identity data is stored in a location that's based on the address your organization provided when you subscribed to the service.</span></span> <span data-ttu-id="4d205-106">For example, when you subscribed to Office 365 or Azure.</span><span class="sxs-lookup"><span data-stu-id="4d205-106">For example, when you subscribed to Office 365 or Azure.</span></span> <span data-ttu-id="4d205-107">For specific info about where your identity data is stored, you can use the [Where is your data located?](https://www.microsoft.com/trustcenter/privacy/where-your-data-is-located) section of the Microsoft Trust Center.</span><span class="sxs-lookup"><span data-stu-id="4d205-107">For specific info about where your identity data is stored, you can use the [Where is your data located?](https://www.microsoft.com/trustcenter/privacy/where-your-data-is-located) section of the Microsoft Trust Center.</span></span>

<span data-ttu-id="4d205-108">While most Azure AD-related European identity data stays in European datacenters, there are five user-related attributes that are typically stored in U.S. datacenters.</span><span class="sxs-lookup"><span data-stu-id="4d205-108">While most Azure AD-related European identity data stays in European datacenters, there are five user-related attributes that are typically stored in U.S. datacenters.</span></span> <span data-ttu-id="4d205-109">These attributes are GivenName, Surname, userPrincipalName, Domain, and PasswordHash.</span><span class="sxs-lookup"><span data-stu-id="4d205-109">These attributes are GivenName, Surname, userPrincipalName, Domain, and PasswordHash.</span></span> <span data-ttu-id="4d205-110">The PasswordHash attribute can be an exception and not stored in the U.S. if someone uses an on-premises, federated authentication method that stops the PasswordHash value from syncing with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d205-110">The PasswordHash attribute can be an exception and not stored in the U.S. if someone uses an on-premises, federated authentication method that stops the PasswordHash value from syncing with Azure AD.</span></span> <span data-ttu-id="4d205-111">Additionally, there is some operational, service-specific data that's required for normal Azure AD operation, which is stored in the U.S. and doesn't include any personal data.</span><span class="sxs-lookup"><span data-stu-id="4d205-111">Additionally, there is some operational, service-specific data that's required for normal Azure AD operation, which is stored in the U.S. and doesn't include any personal data.</span></span>

## <a name="data-stored-outside-of-european-datacenters-for-european-customers"></a><span data-ttu-id="4d205-112">Data stored outside of European datacenters for European customers</span><span class="sxs-lookup"><span data-stu-id="4d205-112">Data stored outside of European datacenters for European customers</span></span>

<span data-ttu-id="4d205-113">Most Azure AD-related European identity data, for organizations with European-based addresses, stays in European datacenters.</span><span class="sxs-lookup"><span data-stu-id="4d205-113">Most Azure AD-related European identity data, for organizations with European-based addresses, stays in European datacenters.</span></span> <span data-ttu-id="4d205-114">Azure AD data that's not stored in European datacenters, includes:</span><span class="sxs-lookup"><span data-stu-id="4d205-114">Azure AD data that's not stored in European datacenters, includes:</span></span>

- <span data-ttu-id="4d205-115">**Identity-related attributes**</span><span class="sxs-lookup"><span data-stu-id="4d205-115">**Identity-related attributes**</span></span>

    <span data-ttu-id="4d205-116">The following identity-related attributes will be replicated to the United States:</span><span class="sxs-lookup"><span data-stu-id="4d205-116">The following identity-related attributes will be replicated to the United States:</span></span>

    - <span data-ttu-id="4d205-117">GivenName</span><span class="sxs-lookup"><span data-stu-id="4d205-117">GivenName</span></span>
    - <span data-ttu-id="4d205-118">Surname</span><span class="sxs-lookup"><span data-stu-id="4d205-118">Surname</span></span>
    - <span data-ttu-id="4d205-119">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="4d205-119">userPrincipalName</span></span>
    - <span data-ttu-id="4d205-120">Domain</span><span class="sxs-lookup"><span data-stu-id="4d205-120">Domain</span></span>
    - <span data-ttu-id="4d205-121">PasswordHash</span><span class="sxs-lookup"><span data-stu-id="4d205-121">PasswordHash</span></span>
    - <span data-ttu-id="4d205-122">SourceAnchor</span><span class="sxs-lookup"><span data-stu-id="4d205-122">SourceAnchor</span></span>
    - <span data-ttu-id="4d205-123">AccountEnabled</span><span class="sxs-lookup"><span data-stu-id="4d205-123">AccountEnabled</span></span>
    - <span data-ttu-id="4d205-124">PasswordPolicies</span><span class="sxs-lookup"><span data-stu-id="4d205-124">PasswordPolicies</span></span>
    - <span data-ttu-id="4d205-125">StrongAuthenticationRequirement</span><span class="sxs-lookup"><span data-stu-id="4d205-125">StrongAuthenticationRequirement</span></span>
    - <span data-ttu-id="4d205-126">ApplicationPassword</span><span class="sxs-lookup"><span data-stu-id="4d205-126">ApplicationPassword</span></span>
    - <span data-ttu-id="4d205-127">PUID</span><span class="sxs-lookup"><span data-stu-id="4d205-127">PUID</span></span>

- <span data-ttu-id="4d205-128">**Microsoft Azure multi-factor authentication (MFA) and Azure AD self-service password reset (SSPR)**</span><span class="sxs-lookup"><span data-stu-id="4d205-128">**Microsoft Azure multi-factor authentication (MFA) and Azure AD self-service password reset (SSPR)**</span></span>
    
    <span data-ttu-id="4d205-129">MFA stores all user data at-rest in European datacenters.</span><span class="sxs-lookup"><span data-stu-id="4d205-129">MFA stores all user data at-rest in European datacenters.</span></span> <span data-ttu-id="4d205-130">However, some MFA service-specific data is stored in the U.S., including:</span><span class="sxs-lookup"><span data-stu-id="4d205-130">However, some MFA service-specific data is stored in the U.S., including:</span></span>
    
    - <span data-ttu-id="4d205-131">Two-factor authentication and its related personal data might be stored in the U.S. if you're using MFA or SSPR.</span><span class="sxs-lookup"><span data-stu-id="4d205-131">Two-factor authentication and its related personal data might be stored in the U.S. if you're using MFA or SSPR.</span></span>
        - <span data-ttu-id="4d205-132">All two-factor authentication using phone calls or SMS might be completed by U.S. carriers.</span><span class="sxs-lookup"><span data-stu-id="4d205-132">All two-factor authentication using phone calls or SMS might be completed by U.S. carriers.</span></span>
        - <span data-ttu-id="4d205-133">Push notifications using the Microsoft Authenticator app require notifications from the manufacturer's notification service (Apple or Google), which might be outside Europe.</span><span class="sxs-lookup"><span data-stu-id="4d205-133">Push notifications using the Microsoft Authenticator app require notifications from the manufacturer's notification service (Apple or Google), which might be outside Europe.</span></span>
        - <span data-ttu-id="4d205-134">OATH codes are always validated in the U.S.</span><span class="sxs-lookup"><span data-stu-id="4d205-134">OATH codes are always validated in the U.S.</span></span> 
    - <span data-ttu-id="4d205-135">Some MFA and SSPR logs are stored in the U.S. for 30 days, regardless of authentication type.</span><span class="sxs-lookup"><span data-stu-id="4d205-135">Some MFA and SSPR logs are stored in the U.S. for 30 days, regardless of authentication type.</span></span>

- <span data-ttu-id="4d205-136">**Microsoft Azure Active Directory B2C (Azure AD B2C)**</span><span class="sxs-lookup"><span data-stu-id="4d205-136">**Microsoft Azure Active Directory B2C (Azure AD B2C)**</span></span>

    <span data-ttu-id="4d205-137">Azure AD B2C stores all user data at-rest in European datacenters.</span><span class="sxs-lookup"><span data-stu-id="4d205-137">Azure AD B2C stores all user data at-rest in European datacenters.</span></span> <span data-ttu-id="4d205-138">However, operational logs (with personal data removed) stay at the location from where the person is accessing the services.</span><span class="sxs-lookup"><span data-stu-id="4d205-138">However, operational logs (with personal data removed) stay at the location from where the person is accessing the services.</span></span> <span data-ttu-id="4d205-139">For example, if a B2C user accesses the service in the U.S., the operational logs stay in the U.S. Additionally, all policy configuration data not containing personal data is stored only in the U.S. For more info about policy configurations, see the [Azure Active Directory B2C: Built-in policies](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies) article.</span><span class="sxs-lookup"><span data-stu-id="4d205-139">For example, if a B2C user accesses the service in the U.S., the operational logs stay in the U.S. Additionally, all policy configuration data not containing personal data is stored only in the U.S. For more info about policy configurations, see the [Azure Active Directory B2C: Built-in policies](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies) article.</span></span>

- <span data-ttu-id="4d205-140">**Microsoft Azure Active Directory B2B (Azure AD B2B)**</span><span class="sxs-lookup"><span data-stu-id="4d205-140">**Microsoft Azure Active Directory B2B (Azure AD B2B)**</span></span> 
    
    <span data-ttu-id="4d205-141">Azure AD B2B stores all user data at-rest in European datacenters.</span><span class="sxs-lookup"><span data-stu-id="4d205-141">Azure AD B2B stores all user data at-rest in European datacenters.</span></span> <span data-ttu-id="4d205-142">However, B2B stores its non-personal metadata in tables within U.S. datacenters.</span><span class="sxs-lookup"><span data-stu-id="4d205-142">However, B2B stores its non-personal metadata in tables within U.S. datacenters.</span></span> <span data-ttu-id="4d205-143">This table includes fields like redeemUrl, invitationTicket, resource tenant Id, InviteRedirectUrl, and InviterAppId.</span><span class="sxs-lookup"><span data-stu-id="4d205-143">This table includes fields like redeemUrl, invitationTicket, resource tenant Id, InviteRedirectUrl, and InviterAppId.</span></span>

- <span data-ttu-id="4d205-144">**Microsoft Azure Active Directory Domain Services (Azure AD DS)**</span><span class="sxs-lookup"><span data-stu-id="4d205-144">**Microsoft Azure Active Directory Domain Services (Azure AD DS)**</span></span>

    <span data-ttu-id="4d205-145">Azure AD DS stores user data in the same location as the customer-selected Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="4d205-145">Azure AD DS stores user data in the same location as the customer-selected Azure Virtual Network.</span></span> <span data-ttu-id="4d205-146">So, if the network is outside Europe, the data is replicated and stored outside Europe.</span><span class="sxs-lookup"><span data-stu-id="4d205-146">So, if the network is outside Europe, the data is replicated and stored outside Europe.</span></span>

- <span data-ttu-id="4d205-147">**Services and apps integrated with Azure AD**</span><span class="sxs-lookup"><span data-stu-id="4d205-147">**Services and apps integrated with Azure AD**</span></span>

    <span data-ttu-id="4d205-148">Any services and apps that integrate with Azure AD have access to identity data.</span><span class="sxs-lookup"><span data-stu-id="4d205-148">Any services and apps that integrate with Azure AD have access to identity data.</span></span> <span data-ttu-id="4d205-149">Evaluate each service and app to determine how identity data is processed by that specific service and app, and whether they meet your company's data storage requirements.</span><span class="sxs-lookup"><span data-stu-id="4d205-149">Evaluate each service and app to determine how identity data is processed by that specific service and app, and whether they meet your company's data storage requirements.</span></span>

    <span data-ttu-id="4d205-150">For more information about Microsoft services' data residency, see the [Where is your data located?](https://www.microsoft.com/trustcenter/privacy/where-your-data-is-located) section of the Microsoft Trust Center.</span><span class="sxs-lookup"><span data-stu-id="4d205-150">For more information about Microsoft services' data residency, see the [Where is your data located?](https://www.microsoft.com/trustcenter/privacy/where-your-data-is-located) section of the Microsoft Trust Center.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d205-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d205-151">Next steps</span></span>
<span data-ttu-id="4d205-152">For more information about any of the features and functionality described above, see these articles.</span><span class="sxs-lookup"><span data-stu-id="4d205-152">For more information about any of the features and functionality described above, see these articles.</span></span>
- [<span data-ttu-id="4d205-153">Get started with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4d205-153">Get started with Azure Active Directory</span></span>](get-started-azure-ad.md)
- [<span data-ttu-id="4d205-154">What is Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="4d205-154">What is Multi-Factor Authentication?</span></span>](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication)
- [<span data-ttu-id="4d205-155">Azure AD self-service password reset</span><span class="sxs-lookup"><span data-stu-id="4d205-155">Azure AD self-service password reset</span></span>](https://docs.microsoft.com/azure/active-directory/authentication/active-directory-passwords-overview)
- [<span data-ttu-id="4d205-156">What is Azure Active Directory B2C?</span><span class="sxs-lookup"><span data-stu-id="4d205-156">What is Azure Active Directory B2C?</span></span>](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview)
- [<span data-ttu-id="4d205-157">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="4d205-157">What is Azure AD B2B collaboration?</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)
- [<span data-ttu-id="4d205-158">Azure Active Directory (AD) Domain Services</span><span class="sxs-lookup"><span data-stu-id="4d205-158">Azure Active Directory (AD) Domain Services</span></span>](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview)
