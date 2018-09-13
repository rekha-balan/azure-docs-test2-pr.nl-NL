---
title: What is Self-Service Signup for Azure? | Microsoft Docs
description: An overview self-service signup for Azure, how to manage the signup process, and how to take over a DNS domain name.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/13/2017
ms.author: curtand
ms.openlocfilehash: 6734fedeb6e08ea4f7b203f885cbe01d60c03b48
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550721"
---
# <a name="what-is-self-service-signup-for-azure"></a><span data-ttu-id="c8b8a-104">What is Self-Service Signup for Azure?</span><span class="sxs-lookup"><span data-stu-id="c8b8a-104">What is Self-Service Signup for Azure?</span></span>
<span data-ttu-id="c8b8a-105">This topic explains the self-service signup process and how to take over a DNS domain name.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-105">This topic explains the self-service signup process and how to take over a DNS domain name.</span></span>  

## <a name="why-use-self-service-signup"></a><span data-ttu-id="c8b8a-106">Why use self-service signup?</span><span class="sxs-lookup"><span data-stu-id="c8b8a-106">Why use self-service signup?</span></span>
* <span data-ttu-id="c8b8a-107">Get customers to services they want faster.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-107">Get customers to services they want faster.</span></span>
* <span data-ttu-id="c8b8a-108">Create email-based offers for a service.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-108">Create email-based offers for a service.</span></span>
* <span data-ttu-id="c8b8a-109">Create email-based signup flows which quickly allow users to create identities using their easy-to-remember work email aliases.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-109">Create email-based signup flows which quickly allow users to create identities using their easy-to-remember work email aliases.</span></span>
* <span data-ttu-id="c8b8a-110">Unmanaged Azure directories can be made into managed directories later and be reused for other services.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-110">Unmanaged Azure directories can be made into managed directories later and be reused for other services.</span></span>

## <a name="terms-and-definitions"></a><span data-ttu-id="c8b8a-111">Terms and Definitions</span><span class="sxs-lookup"><span data-stu-id="c8b8a-111">Terms and Definitions</span></span>
* <span data-ttu-id="c8b8a-112">**Self-service sign up**: This is the method by which a user signs up for a cloud service and has an identity automatically created for them in Azure Active Directory (Azure AD) based on their email domain.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-112">**Self-service sign up**: This is the method by which a user signs up for a cloud service and has an identity automatically created for them in Azure Active Directory (Azure AD) based on their email domain.</span></span>
* <span data-ttu-id="c8b8a-113">**Unmanaged Azure directory**: This is the directory where that identity is created.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-113">**Unmanaged Azure directory**: This is the directory where that identity is created.</span></span> <span data-ttu-id="c8b8a-114">An unmanaged directory is a directory that has no global administrator.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-114">An unmanaged directory is a directory that has no global administrator.</span></span>
* <span data-ttu-id="c8b8a-115">**Email-verified user**: This is a type of user account in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-115">**Email-verified user**: This is a type of user account in Azure AD.</span></span> <span data-ttu-id="c8b8a-116">A user who has an identity created automatically after signing up for a self-service offer is known as an email-verified user.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-116">A user who has an identity created automatically after signing up for a self-service offer is known as an email-verified user.</span></span> <span data-ttu-id="c8b8a-117">An email-verified user is a regular member of a directory tagged with creationmethod=EmailVerified.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-117">An email-verified user is a regular member of a directory tagged with creationmethod=EmailVerified.</span></span>

## <a name="user-experience"></a><span data-ttu-id="c8b8a-118">User experience</span><span class="sxs-lookup"><span data-stu-id="c8b8a-118">User experience</span></span>
<span data-ttu-id="c8b8a-119">For example, let's say a user whose email is Dan@BellowsCollege.com receives sensitive files via email.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-119">For example, let's say a user whose email is Dan@BellowsCollege.com receives sensitive files via email.</span></span> <span data-ttu-id="c8b8a-120">The files have been protected by Azure Rights Management (Azure RMS).</span><span class="sxs-lookup"><span data-stu-id="c8b8a-120">The files have been protected by Azure Rights Management (Azure RMS).</span></span> <span data-ttu-id="c8b8a-121">But Dan's organization, Bellows College, has not signed up for Azure RMS, nor has it deployed Active Directory RMS.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-121">But Dan's organization, Bellows College, has not signed up for Azure RMS, nor has it deployed Active Directory RMS.</span></span> <span data-ttu-id="c8b8a-122">In this case, Dan can sign up for a free subscription to RMS for individuals in order to read the protected files.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-122">In this case, Dan can sign up for a free subscription to RMS for individuals in order to read the protected files.</span></span>

<span data-ttu-id="c8b8a-123">If Dan is the first user with an email address from BellowsCollege.com to sign up for this self-service offering, then an unmanaged directory will be created for BellowsCollege.com in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-123">If Dan is the first user with an email address from BellowsCollege.com to sign up for this self-service offering, then an unmanaged directory will be created for BellowsCollege.com in Azure AD.</span></span> <span data-ttu-id="c8b8a-124">If other users from the BellowsCollege.com domain sign up for this offering or a similar self-service offering, they will also have email-verified user accounts created in the same unmanaged directory in Azure.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-124">If other users from the BellowsCollege.com domain sign up for this offering or a similar self-service offering, they will also have email-verified user accounts created in the same unmanaged directory in Azure.</span></span>

## <a name="admin-experience"></a><span data-ttu-id="c8b8a-125">Admin experience</span><span class="sxs-lookup"><span data-stu-id="c8b8a-125">Admin experience</span></span>
<span data-ttu-id="c8b8a-126">An admin who owns the DNS domain name of an unmanaged Azure directory can take over or merge the directory after proving ownership.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-126">An admin who owns the DNS domain name of an unmanaged Azure directory can take over or merge the directory after proving ownership.</span></span> <span data-ttu-id="c8b8a-127">The next sections explain the admin experience in more detail, but here's a summary:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-127">The next sections explain the admin experience in more detail, but here's a summary:</span></span>

* <span data-ttu-id="c8b8a-128">When you take over an unmanaged Azure directory, you simply become the global administrator of the unmanaged directory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-128">When you take over an unmanaged Azure directory, you simply become the global administrator of the unmanaged directory.</span></span> <span data-ttu-id="c8b8a-129">This is sometimes called an internal takeover.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-129">This is sometimes called an internal takeover.</span></span>
* <span data-ttu-id="c8b8a-130">When you merge an unmanaged Azure directory, you add the DNS domain name of the unmanaged directory to your managed Azure directory and a mapping of users-to-resources is created so users can continue to access services without interruption.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-130">When you merge an unmanaged Azure directory, you add the DNS domain name of the unmanaged directory to your managed Azure directory and a mapping of users-to-resources is created so users can continue to access services without interruption.</span></span> <span data-ttu-id="c8b8a-131">This is sometimes called an external takeover.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-131">This is sometimes called an external takeover.</span></span>

## <a name="what-gets-created-in-azure-active-directory"></a><span data-ttu-id="c8b8a-132">What gets created in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c8b8a-132">What gets created in Azure Active Directory?</span></span>
#### <a name="directory"></a><span data-ttu-id="c8b8a-133">directory</span><span class="sxs-lookup"><span data-stu-id="c8b8a-133">directory</span></span>
* <span data-ttu-id="c8b8a-134">An Azure Active Directory directory for the domain is created, one directory per domain.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-134">An Azure Active Directory directory for the domain is created, one directory per domain.</span></span>
* <span data-ttu-id="c8b8a-135">The Azure AD directory has no global admin.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-135">The Azure AD directory has no global admin.</span></span>

#### <a name="users"></a><span data-ttu-id="c8b8a-136">Users</span><span class="sxs-lookup"><span data-stu-id="c8b8a-136">Users</span></span>
* <span data-ttu-id="c8b8a-137">For each user who signs up, a user object is created in the Azure AD directory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-137">For each user who signs up, a user object is created in the Azure AD directory.</span></span>
* <span data-ttu-id="c8b8a-138">Each user object is marked as external.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-138">Each user object is marked as external.</span></span>
* <span data-ttu-id="c8b8a-139">Each user is given access to the service that they signed up for.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-139">Each user is given access to the service that they signed up for.</span></span>

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a><span data-ttu-id="c8b8a-140">How do I claim a self-service Azure AD directory for a domain I own?</span><span class="sxs-lookup"><span data-stu-id="c8b8a-140">How do I claim a self-service Azure AD directory for a domain I own?</span></span>
<span data-ttu-id="c8b8a-141">You can claim a self-service Azure AD directory by performing domain validation.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-141">You can claim a self-service Azure AD directory by performing domain validation.</span></span> <span data-ttu-id="c8b8a-142">Domain validation proves you own the domain by creating DNS records.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-142">Domain validation proves you own the domain by creating DNS records.</span></span>

<span data-ttu-id="c8b8a-143">There are two ways to do a DNS takeover of an Azure AD directory:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-143">There are two ways to do a DNS takeover of an Azure AD directory:</span></span>

* <span data-ttu-id="c8b8a-144">internal takeover (Admin discovers an unmanaged Azure directory, and wants to turn into a managed directory)</span><span class="sxs-lookup"><span data-stu-id="c8b8a-144">internal takeover (Admin discovers an unmanaged Azure directory, and wants to turn into a managed directory)</span></span>
* <span data-ttu-id="c8b8a-145">external takeover (Admin tries to add a new domain to their managed Azure directory)</span><span class="sxs-lookup"><span data-stu-id="c8b8a-145">external takeover (Admin tries to add a new domain to their managed Azure directory)</span></span>

<span data-ttu-id="c8b8a-146">You might be interested in validating that you own a domain because you are taking over an unmanaged directory after a user performed self-service signup, or you might be adding a new domain to an existing managed directory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-146">You might be interested in validating that you own a domain because you are taking over an unmanaged directory after a user performed self-service signup, or you might be adding a new domain to an existing managed directory.</span></span> <span data-ttu-id="c8b8a-147">For example, you have a domain named contoso.com and you want to add a new domain named contoso.co.uk or contoso.uk.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-147">For example, you have a domain named contoso.com and you want to add a new domain named contoso.co.uk or contoso.uk.</span></span>

## <a name="what-is-domain-takeover"></a><span data-ttu-id="c8b8a-148">What is domain takeover?</span><span class="sxs-lookup"><span data-stu-id="c8b8a-148">What is domain takeover?</span></span>
<span data-ttu-id="c8b8a-149">This section covers how to validate that you own a domain</span><span class="sxs-lookup"><span data-stu-id="c8b8a-149">This section covers how to validate that you own a domain</span></span>

### <a name="what-is-domain-validation-and-why-is-it-used"></a><span data-ttu-id="c8b8a-150">What is domain validation and why is it used?</span><span class="sxs-lookup"><span data-stu-id="c8b8a-150">What is domain validation and why is it used?</span></span>
<span data-ttu-id="c8b8a-151">In order to perform operations on a directory, Azure AD requires that you validate ownership of the DNS domain.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-151">In order to perform operations on a directory, Azure AD requires that you validate ownership of the DNS domain.</span></span>  <span data-ttu-id="c8b8a-152">Validation of the domain allows you to claim the directory and either promote the self-service directory to a managed directory, or merge the self-service directory into an existing managed directory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-152">Validation of the domain allows you to claim the directory and either promote the self-service directory to a managed directory, or merge the self-service directory into an existing managed directory.</span></span>

## <a name="examples-of-domain-validation"></a><span data-ttu-id="c8b8a-153">Examples of domain validation</span><span class="sxs-lookup"><span data-stu-id="c8b8a-153">Examples of domain validation</span></span>
<span data-ttu-id="c8b8a-154">There are two ways to do a DNS takeover of a directory:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-154">There are two ways to do a DNS takeover of a directory:</span></span>

* <span data-ttu-id="c8b8a-155">internal takeover  (For example, an admin discovers a self-service, unmanaged directory, and wants to turn into managed directory)</span><span class="sxs-lookup"><span data-stu-id="c8b8a-155">internal takeover  (For example, an admin discovers a self-service, unmanaged directory, and wants to turn into managed directory)</span></span>
* <span data-ttu-id="c8b8a-156">external takeover (For example, a admin tries to add a new domain to a managed directory)</span><span class="sxs-lookup"><span data-stu-id="c8b8a-156">external takeover (For example, a admin tries to add a new domain to a managed directory)</span></span>

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-to-be-a-managed-directory"></a><span data-ttu-id="c8b8a-157">Internal Takeover - promote a self-service, unmanaged directory to be a managed directory</span><span class="sxs-lookup"><span data-stu-id="c8b8a-157">Internal Takeover - promote a self-service, unmanaged directory to be a managed directory</span></span>
<span data-ttu-id="c8b8a-158">When you do internal takeover, the directory gets converted from an unmanaged directory to a managed directory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-158">When you do internal takeover, the directory gets converted from an unmanaged directory to a managed directory.</span></span> <span data-ttu-id="c8b8a-159">You need to complete DNS domain name validation, where you create an MX record or a TXT record in the DNS zone.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-159">You need to complete DNS domain name validation, where you create an MX record or a TXT record in the DNS zone.</span></span> <span data-ttu-id="c8b8a-160">That action:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-160">That action:</span></span>

* <span data-ttu-id="c8b8a-161">Validates that you own the domain</span><span class="sxs-lookup"><span data-stu-id="c8b8a-161">Validates that you own the domain</span></span>
* <span data-ttu-id="c8b8a-162">Makes the directory managed</span><span class="sxs-lookup"><span data-stu-id="c8b8a-162">Makes the directory managed</span></span>
* <span data-ttu-id="c8b8a-163">Makes you the global admin of the directory</span><span class="sxs-lookup"><span data-stu-id="c8b8a-163">Makes you the global admin of the directory</span></span>

<span data-ttu-id="c8b8a-164">Let's say an IT administrator from Bellows College discovers that users from the school have signed up for self-service offerings.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-164">Let's say an IT administrator from Bellows College discovers that users from the school have signed up for self-service offerings.</span></span> <span data-ttu-id="c8b8a-165">As the registered owner of the DNS name BellowsCollege.com, the IT administrator can validate ownership of the DNS name in Azure and then take over the unmanaged directory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-165">As the registered owner of the DNS name BellowsCollege.com, the IT administrator can validate ownership of the DNS name in Azure and then take over the unmanaged directory.</span></span> <span data-ttu-id="c8b8a-166">The directory then becomes a managed directory, and the IT administrator is assigned the global administrator role for the BellowsCollege.com directory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-166">The directory then becomes a managed directory, and the IT administrator is assigned the global administrator role for the BellowsCollege.com directory.</span></span>

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a><span data-ttu-id="c8b8a-167">External Takeover - merge a self-service directory into an existing managed directory</span><span class="sxs-lookup"><span data-stu-id="c8b8a-167">External Takeover - merge a self-service directory into an existing managed directory</span></span>
<span data-ttu-id="c8b8a-168">In an external takeover, you already have a managed directory and you want all users and groups from an unmanaged directory to join that managed directory, rather than own two separate directories.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-168">In an external takeover, you already have a managed directory and you want all users and groups from an unmanaged directory to join that managed directory, rather than own two separate directories.</span></span>

<span data-ttu-id="c8b8a-169">As an admin of a managed directory, you add a domain, and that domain happens to have an unmanaged directory associated with it.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-169">As an admin of a managed directory, you add a domain, and that domain happens to have an unmanaged directory associated with it.</span></span>

<span data-ttu-id="c8b8a-170">For example, let's say you are an IT administrator and you already have a managed directory for Contoso.com, a domain name that is registered to your organization.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-170">For example, let's say you are an IT administrator and you already have a managed directory for Contoso.com, a domain name that is registered to your organization.</span></span> <span data-ttu-id="c8b8a-171">You discover that users from your organization have performed self-service sign up for an offering by using email domain name user@contoso.co.uk, which is another domain name that your organization owns.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-171">You discover that users from your organization have performed self-service sign up for an offering by using email domain name user@contoso.co.uk, which is another domain name that your organization owns.</span></span> <span data-ttu-id="c8b8a-172">Those users currently have accounts in an unmanaged directory for contoso.co.uk.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-172">Those users currently have accounts in an unmanaged directory for contoso.co.uk.</span></span>

<span data-ttu-id="c8b8a-173">You don't want to manage two separate directories, so you merge the unmanaged directory for contoso.co.uk into your existing IT managed directory for contoso.com.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-173">You don't want to manage two separate directories, so you merge the unmanaged directory for contoso.co.uk into your existing IT managed directory for contoso.com.</span></span>

<span data-ttu-id="c8b8a-174">External takeover follows the same DNS validation process as internal takeover.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-174">External takeover follows the same DNS validation process as internal takeover.</span></span>  <span data-ttu-id="c8b8a-175">Difference being: users and services are remapped to the IT managed directory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-175">Difference being: users and services are remapped to the IT managed directory.</span></span>

#### <a name="whats-the-impact-of-performing-an-external-takeover"></a><span data-ttu-id="c8b8a-176">What's the impact of performing an external takeover?</span><span class="sxs-lookup"><span data-stu-id="c8b8a-176">What's the impact of performing an external takeover?</span></span>
<span data-ttu-id="c8b8a-177">With an external takeover, a mapping of users-to-resources is created so users can continue to access services without interruption.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-177">With an external takeover, a mapping of users-to-resources is created so users can continue to access services without interruption.</span></span> <span data-ttu-id="c8b8a-178">Many applications, including RMS for individuals, handle the mapping of users-to-resources well, and users can continue to access those services without change.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-178">Many applications, including RMS for individuals, handle the mapping of users-to-resources well, and users can continue to access those services without change.</span></span> <span data-ttu-id="c8b8a-179">If an application does not handle the mapping of users-to-resources effectively, external takeover may be explicitly blocked to prevent users from a poor experience.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-179">If an application does not handle the mapping of users-to-resources effectively, external takeover may be explicitly blocked to prevent users from a poor experience.</span></span>

#### <a name="directory-takeover-support-by-service"></a><span data-ttu-id="c8b8a-180">directory takeover support by service</span><span class="sxs-lookup"><span data-stu-id="c8b8a-180">directory takeover support by service</span></span>
<span data-ttu-id="c8b8a-181">Currently the following services support takeover:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-181">Currently the following services support takeover:</span></span>

* <span data-ttu-id="c8b8a-182">RMS</span><span class="sxs-lookup"><span data-stu-id="c8b8a-182">RMS</span></span>

<span data-ttu-id="c8b8a-183">The following services will soon be supporting takeover:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-183">The following services will soon be supporting takeover:</span></span>

* <span data-ttu-id="c8b8a-184">PowerBI</span><span class="sxs-lookup"><span data-stu-id="c8b8a-184">PowerBI</span></span>

<span data-ttu-id="c8b8a-185">The following do not and require additional admin action to migrate user data after an external takeover.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-185">The following do not and require additional admin action to migrate user data after an external takeover.</span></span>

* <span data-ttu-id="c8b8a-186">SharePoint/OneDrive</span><span class="sxs-lookup"><span data-stu-id="c8b8a-186">SharePoint/OneDrive</span></span>

## <a name="how-to-perform-a-dns-domain-name-takeover"></a><span data-ttu-id="c8b8a-187">How to perform a DNS domain name takeover</span><span class="sxs-lookup"><span data-stu-id="c8b8a-187">How to perform a DNS domain name takeover</span></span>
<span data-ttu-id="c8b8a-188">You have a few options for how to perform a domain validation (and do a takeover if you wish):</span><span class="sxs-lookup"><span data-stu-id="c8b8a-188">You have a few options for how to perform a domain validation (and do a takeover if you wish):</span></span>

1. <span data-ttu-id="c8b8a-189">Azure Management Portal</span><span class="sxs-lookup"><span data-stu-id="c8b8a-189">Azure Management Portal</span></span>

   <span data-ttu-id="c8b8a-190">A takeover is triggered by doing a domain addition.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-190">A takeover is triggered by doing a domain addition.</span></span>  <span data-ttu-id="c8b8a-191">If a directory already exists for the domain, you'll have the option to perform an external takeover.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-191">If a directory already exists for the domain, you'll have the option to perform an external takeover.</span></span>

   <span data-ttu-id="c8b8a-192">Sign in to the Azure portal using your credentials.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-192">Sign in to the Azure portal using your credentials.</span></span>  <span data-ttu-id="c8b8a-193">Navigate to your existing directory and then to **Add domain**.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-193">Navigate to your existing directory and then to **Add domain**.</span></span>
2. <span data-ttu-id="c8b8a-194">Office 365</span><span class="sxs-lookup"><span data-stu-id="c8b8a-194">Office 365</span></span>

   <span data-ttu-id="c8b8a-195">You can use the options on the [Manage domains](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) page in Office 365 to work with your domains and DNS records.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-195">You can use the options on the [Manage domains](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) page in Office 365 to work with your domains and DNS records.</span></span> <span data-ttu-id="c8b8a-196">See [Verify your domain in Office 365](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).</span><span class="sxs-lookup"><span data-stu-id="c8b8a-196">See [Verify your domain in Office 365](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).</span></span>
3. <span data-ttu-id="c8b8a-197">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8b8a-197">Windows PowerShell</span></span>

   <span data-ttu-id="c8b8a-198">The following steps are required to perform a validation using Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-198">The following steps are required to perform a validation using Windows PowerShell.</span></span>

   | <span data-ttu-id="c8b8a-199">Step</span><span class="sxs-lookup"><span data-stu-id="c8b8a-199">Step</span></span> | <span data-ttu-id="c8b8a-200">Cmdlet to use</span><span class="sxs-lookup"><span data-stu-id="c8b8a-200">Cmdlet to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="c8b8a-201">Create a credential object</span><span class="sxs-lookup"><span data-stu-id="c8b8a-201">Create a credential object</span></span> |<span data-ttu-id="c8b8a-202">Get-Credential</span><span class="sxs-lookup"><span data-stu-id="c8b8a-202">Get-Credential</span></span> |
   | <span data-ttu-id="c8b8a-203">Connect to Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8b8a-203">Connect to Azure AD</span></span> |<span data-ttu-id="c8b8a-204">Connect-MsolService</span><span class="sxs-lookup"><span data-stu-id="c8b8a-204">Connect-MsolService</span></span> |
   | <span data-ttu-id="c8b8a-205">get a list of domains</span><span class="sxs-lookup"><span data-stu-id="c8b8a-205">get a list of domains</span></span> |<span data-ttu-id="c8b8a-206">Get-MsolDomain</span><span class="sxs-lookup"><span data-stu-id="c8b8a-206">Get-MsolDomain</span></span> |
   | <span data-ttu-id="c8b8a-207">Create a challenge</span><span class="sxs-lookup"><span data-stu-id="c8b8a-207">Create a challenge</span></span> |<span data-ttu-id="c8b8a-208">Get-MsolDomainVerificationDns</span><span class="sxs-lookup"><span data-stu-id="c8b8a-208">Get-MsolDomainVerificationDns</span></span> |
   | <span data-ttu-id="c8b8a-209">Create DNS record</span><span class="sxs-lookup"><span data-stu-id="c8b8a-209">Create DNS record</span></span> |<span data-ttu-id="c8b8a-210">Do this on your DNS server</span><span class="sxs-lookup"><span data-stu-id="c8b8a-210">Do this on your DNS server</span></span> |
   | <span data-ttu-id="c8b8a-211">Verify the challenge</span><span class="sxs-lookup"><span data-stu-id="c8b8a-211">Verify the challenge</span></span> |<span data-ttu-id="c8b8a-212">Confirm-MsolEmailVerifiedDomain</span><span class="sxs-lookup"><span data-stu-id="c8b8a-212">Confirm-MsolEmailVerifiedDomain</span></span> |

<span data-ttu-id="c8b8a-213">For example:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-213">For example:</span></span>

1. <span data-ttu-id="c8b8a-214">Connect to Azure AD using the credentials that were used to respond to the self-service offering:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-214">Connect to Azure AD using the credentials that were used to respond to the self-service offering:</span></span>

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. <span data-ttu-id="c8b8a-215">Get a list of domains:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-215">Get a list of domains:</span></span>

    <span data-ttu-id="c8b8a-216">Get-MsolDomain</span><span class="sxs-lookup"><span data-stu-id="c8b8a-216">Get-MsolDomain</span></span>
3. <span data-ttu-id="c8b8a-217">Then run the Get-MsolDomainVerificationDns cmdlet to create a challenge:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-217">Then run the Get-MsolDomainVerificationDns cmdlet to create a challenge:</span></span>

    <span data-ttu-id="c8b8a-218">Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord</span><span class="sxs-lookup"><span data-stu-id="c8b8a-218">Get-MsolDomainVerificationDns –DomainName *your_domain_name* –Mode DnsTxtRecord</span></span>

    <span data-ttu-id="c8b8a-219">For example:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-219">For example:</span></span>

    <span data-ttu-id="c8b8a-220">Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord</span><span class="sxs-lookup"><span data-stu-id="c8b8a-220">Get-MsolDomainVerificationDns –DomainName contoso.com –Mode DnsTxtRecord</span></span>
4. <span data-ttu-id="c8b8a-221">Copy the value (the challenge) that is returned from this command.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-221">Copy the value (the challenge) that is returned from this command.</span></span>

    <span data-ttu-id="c8b8a-222">For example:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-222">For example:</span></span>

    <span data-ttu-id="c8b8a-223">MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9</span><span class="sxs-lookup"><span data-stu-id="c8b8a-223">MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9</span></span>
5. <span data-ttu-id="c8b8a-224">In your public DNS namespace, create a DNS txt record that contains the value that you copied in the previous step.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-224">In your public DNS namespace, create a DNS txt record that contains the value that you copied in the previous step.</span></span>

    <span data-ttu-id="c8b8a-225">The name for this record is the name of the parent domain, so if you create this resource record by using the DNS role from Windows Server, leave the Record name blank and just paste the value into the Text box</span><span class="sxs-lookup"><span data-stu-id="c8b8a-225">The name for this record is the name of the parent domain, so if you create this resource record by using the DNS role from Windows Server, leave the Record name blank and just paste the value into the Text box</span></span>
6. <span data-ttu-id="c8b8a-226">Run the Confirm-MsolDomain cmdlet to verify the challenge:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-226">Run the Confirm-MsolDomain cmdlet to verify the challenge:</span></span>

    <span data-ttu-id="c8b8a-227">Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*</span><span class="sxs-lookup"><span data-stu-id="c8b8a-227">Confirm-MsolEmailVerifiedDomain -DomainName *your_domain_name*</span></span>

    <span data-ttu-id="c8b8a-228">for example:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-228">for example:</span></span>

    <span data-ttu-id="c8b8a-229">Confirm-MsolEmailVerifiedDomain -DomainName contoso.com</span><span class="sxs-lookup"><span data-stu-id="c8b8a-229">Confirm-MsolEmailVerifiedDomain -DomainName contoso.com</span></span>

<span data-ttu-id="c8b8a-230">A successful challenge returns you to the prompt without an error.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-230">A successful challenge returns you to the prompt without an error.</span></span>

## <a name="how-do-i-control-self-service-settings"></a><span data-ttu-id="c8b8a-231">How do I control self-service settings?</span><span class="sxs-lookup"><span data-stu-id="c8b8a-231">How do I control self-service settings?</span></span>
<span data-ttu-id="c8b8a-232">Admins have two self-service controls today.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-232">Admins have two self-service controls today.</span></span> <span data-ttu-id="c8b8a-233">They can control:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-233">They can control:</span></span>

* <span data-ttu-id="c8b8a-234">Whether or not users can join the directory via email.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-234">Whether or not users can join the directory via email.</span></span>
* <span data-ttu-id="c8b8a-235">Whether or not users can license themselves for applications and services.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-235">Whether or not users can license themselves for applications and services.</span></span>

### <a name="how-can-i-control-these-capabilities"></a><span data-ttu-id="c8b8a-236">How can I control these capabilities?</span><span class="sxs-lookup"><span data-stu-id="c8b8a-236">How can I control these capabilities?</span></span>
<span data-ttu-id="c8b8a-237">An admin can configure these capabilities using these Azure AD cmdlet Set-MsolCompanySettings parameters:</span><span class="sxs-lookup"><span data-stu-id="c8b8a-237">An admin can configure these capabilities using these Azure AD cmdlet Set-MsolCompanySettings parameters:</span></span>

* <span data-ttu-id="c8b8a-238">**AllowEmailVerifiedUsers** controls whether a user can create or join an unmanaged directory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-238">**AllowEmailVerifiedUsers** controls whether a user can create or join an unmanaged directory.</span></span> <span data-ttu-id="c8b8a-239">If you set that parameter to $false, no email-verified users can join the directory.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-239">If you set that parameter to $false, no email-verified users can join the directory.</span></span>
* <span data-ttu-id="c8b8a-240">**AllowAdHocSubscriptions** controls the ability for users to perform self-service sign up.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-240">**AllowAdHocSubscriptions** controls the ability for users to perform self-service sign up.</span></span> <span data-ttu-id="c8b8a-241">If you set that parameter to $false, no users can perform self-service signup.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-241">If you set that parameter to $false, no users can perform self-service signup.</span></span>

### <a name="how-do-the-controls-work-together"></a><span data-ttu-id="c8b8a-242">How do the controls work together?</span><span class="sxs-lookup"><span data-stu-id="c8b8a-242">How do the controls work together?</span></span>
<span data-ttu-id="c8b8a-243">These two parameters can be used in conjunction to define more precise control over self-service sign up.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-243">These two parameters can be used in conjunction to define more precise control over self-service sign up.</span></span> <span data-ttu-id="c8b8a-244">For example, the following command will allow users to perform self-service sign up, but only if those users already have an account in Azure AD (in other words, users who would need an email-verified account to be created cannot perform self-service sign up):</span><span class="sxs-lookup"><span data-stu-id="c8b8a-244">For example, the following command will allow users to perform self-service sign up, but only if those users already have an account in Azure AD (in other words, users who would need an email-verified account to be created cannot perform self-service sign up):</span></span>

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

<span data-ttu-id="c8b8a-245">The following flowchart explains all the different combinations for these parameters and the resulting conditions for the directory and self-service sign up.</span><span class="sxs-lookup"><span data-stu-id="c8b8a-245">The following flowchart explains all the different combinations for these parameters and the resulting conditions for the directory and self-service sign up.</span></span>

![][1]

<span data-ttu-id="c8b8a-246">For more information and examples of how to use these parameters, see [Set-MsolCompanySettings](https://msdn.microsoft.com/library/azure/dn194127.aspx).</span><span class="sxs-lookup"><span data-stu-id="c8b8a-246">For more information and examples of how to use these parameters, see [Set-MsolCompanySettings](https://msdn.microsoft.com/library/azure/dn194127.aspx).</span></span>

## <a name="see-also"></a><span data-ttu-id="c8b8a-247">See Also</span><span class="sxs-lookup"><span data-stu-id="c8b8a-247">See Also</span></span>
* [<span data-ttu-id="c8b8a-248">How to install and configure Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8b8a-248">How to install and configure Azure PowerShell</span></span>](/powershell/azureps-cmdlets-docs)
* [<span data-ttu-id="c8b8a-249">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c8b8a-249">Azure PowerShell</span></span>](https://msdn.microsoft.com/library/azure/jj156055.aspx)
* [<span data-ttu-id="c8b8a-250">Azure Cmdlet Reference</span><span class="sxs-lookup"><span data-stu-id="c8b8a-250">Azure Cmdlet Reference</span></span>](https://msdn.microsoft.com/library/azure/jj554330.aspx)
* [<span data-ttu-id="c8b8a-251">Set-MsolCompanySettings</span><span class="sxs-lookup"><span data-stu-id="c8b8a-251">Set-MsolCompanySettings</span></span>](https://msdn.microsoft.com/library/azure/dn194127.aspx)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-self-service-signup/SelfServiceSignUpControls.png

