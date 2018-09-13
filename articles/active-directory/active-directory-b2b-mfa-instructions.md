---
title: Conditional access for Azure Active Directory B2B collaboration users | Microsoft Docs
description: Azure Active Directory B2B collaboration supports multi-factor authentication (MFA) for selective access to your corporate applications
services: active-directory
documentationcenter: ''
author: sasubram
manager: femila
editor: ''
tags: ''
ms.assetid: ''
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: fac4657e9b78e900c052384e212aa9f3915f970d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549542"
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="bbc6a-103">Conditional access for B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="bbc6a-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="bbc6a-104">Multi-factor authentication for B2B users</span><span class="sxs-lookup"><span data-stu-id="bbc6a-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="bbc6a-105">With Azure AD B2B collaboration, organizations uniquely have the ability to enforce multi-factor authentication policies for B2B users.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-105">With Azure AD B2B collaboration, organizations uniquely have the ability to enforce multi-factor authentication policies for B2B users.</span></span> <span data-ttu-id="bbc6a-106">These policies can be enforced at the tenant level, app level, or individual user level, the same way that these policies can be enabled for full-time employees and members of the organization.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-106">These policies can be enforced at the tenant level, app level, or individual user level, the same way that these policies can be enabled for full-time employees and members of the organization.</span></span> <span data-ttu-id="bbc6a-107">MFA policies are enforced at the resource organization.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-107">MFA policies are enforced at the resource organization.</span></span>

<span data-ttu-id="bbc6a-108">This means:</span><span class="sxs-lookup"><span data-stu-id="bbc6a-108">This means:</span></span>
1. <span data-ttu-id="bbc6a-109">Admin or information worker in Company A invites user from company B to an application Foo in Company A.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-109">Admin or information worker in Company A invites user from company B to an application Foo in Company A.</span></span>
2. <span data-ttu-id="bbc6a-110">Application *Foo* in company A is configured to require MFA on access.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-110">Application *Foo* in company A is configured to require MFA on access.</span></span>
3. <span data-ttu-id="bbc6a-111">When user from company B attempts to access app Foo from company A tenant, they will be asked to complete an MFA challenge as required by company A's MFA policy.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-111">When user from company B attempts to access app Foo from company A tenant, they will be asked to complete an MFA challenge as required by company A's MFA policy.</span></span>
4. <span data-ttu-id="bbc6a-112">User can set up their MFA with company A, choose their MFA option</span><span class="sxs-lookup"><span data-stu-id="bbc6a-112">User can set up their MFA with company A, choose their MFA option</span></span>
5. <span data-ttu-id="bbc6a-113">This will work for any identity (Azure AD or MSA for example if users in Company B authenticate using social ID)</span><span class="sxs-lookup"><span data-stu-id="bbc6a-113">This will work for any identity (Azure AD or MSA for example if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="bbc6a-114">Company A will need to have adequate premium Azure AD SKUs which support MFA.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-114">Company A will need to have adequate premium Azure AD SKUs which support MFA.</span></span> <span data-ttu-id="bbc6a-115">The user from Company B will consume this license from Company A.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-115">The user from Company B will consume this license from Company A.</span></span>

<span data-ttu-id="bbc6a-116">In summary, the inviting tenancy is *always* responsible for MFA of B2B collaboration users from the partner organization, not the partner organization itself (even if it has MFA capabilities).</span><span class="sxs-lookup"><span data-stu-id="bbc6a-116">In summary, the inviting tenancy is *always* responsible for MFA of B2B collaboration users from the partner organization, not the partner organization itself (even if it has MFA capabilities).</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="bbc6a-117">Setting up MFA for B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="bbc6a-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="bbc6a-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span><span class="sxs-lookup"><span data-stu-id="bbc6a-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="bbc6a-119">B2B users MFA experience for offer redemption</span><span class="sxs-lookup"><span data-stu-id="bbc6a-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="bbc6a-120">Check out the animation below to see the redemption experience, as shown in the following video:</span><span class="sxs-lookup"><span data-stu-id="bbc6a-120">Check out the animation below to see the redemption experience, as shown in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="bbc6a-121">MFA reset for B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="bbc6a-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="bbc6a-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets.</span></span> <span data-ttu-id="bbc6a-123">Therefore, the following PowerShell cmdlets should be used if you want to reset a B2B collaboration user's proof up method.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-123">Therefore, the following PowerShell cmdlets should be used if you want to reset a B2B collaboration user's proof up method.</span></span>

1. <span data-ttu-id="bbc6a-124">Connect to Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbc6a-124">Connect to Azure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="bbc6a-125">Get all users with proof up methods</span><span class="sxs-lookup"><span data-stu-id="bbc6a-125">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="bbc6a-126">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="bbc6a-126">Here is an example:</span></span>

  ```
  PS C:\Users\tjwasserGet-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="bbc6a-127">Reset the MFA method for a specific user.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-127">Reset the MFA method for a specific user.</span></span> <span data-ttu-id="bbc6a-128">You can then use that UserPrincipalName to run the reset command to require the B2B collaboration user to set proof-up methods again.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-128">You can then use that UserPrincipalName to run the reset command to require the B2B collaboration user to set proof-up methods again.</span></span> <span data-ttu-id="bbc6a-129">Example:</span><span class="sxs-lookup"><span data-stu-id="bbc6a-129">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-the-resource-tenancy"></a><span data-ttu-id="bbc6a-130">Why do we perform MFA at the resource tenancy?</span><span class="sxs-lookup"><span data-stu-id="bbc6a-130">Why do we perform MFA at the resource tenancy?</span></span>

<span data-ttu-id="bbc6a-131">In the current release, MFA is always in the resource tenancy.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-131">In the current release, MFA is always in the resource tenancy.</span></span> <span data-ttu-id="bbc6a-132">The reason for this is predictability.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-132">The reason for this is predictability.</span></span>

<span data-ttu-id="bbc6a-133">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-133">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="bbc6a-134">Now, if Contoso has MFA policy enabled for App1 but not App2 – then if we look at the on the Contoso MFA claim in the token to determine whether Sally should MFA in Fabrikam or not, the following issue could happen:</span><span class="sxs-lookup"><span data-stu-id="bbc6a-134">Now, if Contoso has MFA policy enabled for App1 but not App2 – then if we look at the on the Contoso MFA claim in the token to determine whether Sally should MFA in Fabrikam or not, the following issue could happen:</span></span>

* <span data-ttu-id="bbc6a-135">Day 1: Sally has MFA-ed in Contoso because she is accessing App1, then she won’t see the MFA prompt in Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-135">Day 1: Sally has MFA-ed in Contoso because she is accessing App1, then she won’t see the MFA prompt in Fabrikam.</span></span>

* <span data-ttu-id="bbc6a-136">Day 2: Sally has accessed App 2 in Contoso, so now when she accesses Fabrikam, she will have to register for MFA in Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-136">Day 2: Sally has accessed App 2 in Contoso, so now when she accesses Fabrikam, she will have to register for MFA in Fabrikam.</span></span>

<span data-ttu-id="bbc6a-137">This can be quite confusing for Sally and likely will lead to drop in sign-in completions.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-137">This can be quite confusing for Sally and likely will lead to drop in sign-in completions.</span></span>

<span data-ttu-id="bbc6a-138">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-138">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span></span>

<span data-ttu-id="bbc6a-139">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have an MFA set up.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-139">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have an MFA set up.</span></span>

<span data-ttu-id="bbc6a-140">Therefore, the recommendation for MFA for B2B users is to always require resource MFA.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-140">Therefore, the recommendation for MFA for B2B users is to always require resource MFA.</span></span> <span data-ttu-id="bbc6a-141">This could lead to double MFA in some cases, but whenever accessing resource tenancy, the end-users experience is predictable: Sally must register for MFA with the resource tenancy.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-141">This could lead to double MFA in some cases, but whenever accessing resource tenancy, the end-users experience is predictable: Sally must register for MFA with the resource tenancy.</span></span>

### <a name="device-location-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="bbc6a-142">Device, location and risk-based conditional access for B2B users</span><span class="sxs-lookup"><span data-stu-id="bbc6a-142">Device, location and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="bbc6a-143">When the Contoso org enables device based conditional access policies for their corporate data, access is prevented from unmanaged devices (that is, devices that are not managed by the Contoso organization and not compliant with the Contoso device policies).</span><span class="sxs-lookup"><span data-stu-id="bbc6a-143">When the Contoso org enables device based conditional access policies for their corporate data, access is prevented from unmanaged devices (that is, devices that are not managed by the Contoso organization and not compliant with the Contoso device policies).</span></span>

<span data-ttu-id="bbc6a-144">If the B2B user’s device is not managed by Contoso, this means that access of B2B users from the partner organizations will be blocked in whatever context these policies are enforced.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-144">If the B2B user’s device is not managed by Contoso, this means that access of B2B users from the partner organizations will be blocked in whatever context these policies are enforced.</span></span>

<span data-ttu-id="bbc6a-145">It is a high bar to expect users from another organization to have their device managed by the inviting org. Therefore, in future updates, we will be enabling Contoso to trust specific partner’s device compliance status.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-145">It is a high bar to expect users from another organization to have their device managed by the inviting org. Therefore, in future updates, we will be enabling Contoso to trust specific partner’s device compliance status.</span></span> <span data-ttu-id="bbc6a-146">This would allow Contoso to enforce policies where a user from Fabrikam can access Contoso resources if they are using a Fabrikam managed device as well.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-146">This would allow Contoso to enforce policies where a user from Fabrikam can access Contoso resources if they are using a Fabrikam managed device as well.</span></span>

<span data-ttu-id="bbc6a-147">In the meantime, Contoso can create exclusion lists containing specific partner users from the device-based conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-147">In the meantime, Contoso can create exclusion lists containing specific partner users from the device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="bbc6a-148">Location-based conditional access for B2B</span><span class="sxs-lookup"><span data-stu-id="bbc6a-148">Location-based conditional access for B2B</span></span>

<span data-ttu-id="bbc6a-149">Location based conditional access policies can be enforced for B2B users if the inviting organization (for example, Contoso) is able to create a trusted network perimeter (that is, an IP address range) that defines their partner organizations (for example, Fabrikam).</span><span class="sxs-lookup"><span data-stu-id="bbc6a-149">Location based conditional access policies can be enforced for B2B users if the inviting organization (for example, Contoso) is able to create a trusted network perimeter (that is, an IP address range) that defines their partner organizations (for example, Fabrikam).</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="bbc6a-150">Risk-based conditional access for B2B</span><span class="sxs-lookup"><span data-stu-id="bbc6a-150">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="bbc6a-151">Currently, sign-in risk based policies cannot be applied for B2B users, because the risk evaluation is performed at the B2B user’s home organization (in other words, the B2B user’s identity tenancy).</span><span class="sxs-lookup"><span data-stu-id="bbc6a-151">Currently, sign-in risk based policies cannot be applied for B2B users, because the risk evaluation is performed at the B2B user’s home organization (in other words, the B2B user’s identity tenancy).</span></span>

<span data-ttu-id="bbc6a-152">For future updates, we are considering federating the risk score from partners (with the partner’s consent) so that Contoso can protect their externally shared apps and data not just from risks that they know about, but risks that they have no way of knowing about, because they might be occurring elsewhere.</span><span class="sxs-lookup"><span data-stu-id="bbc6a-152">For future updates, we are considering federating the risk score from partners (with the partner’s consent) so that Contoso can protect their externally shared apps and data not just from risks that they know about, but risks that they have no way of knowing about, because they might be occurring elsewhere.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbc6a-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="bbc6a-153">Next steps</span></span>

<span data-ttu-id="bbc6a-154">Browse our other articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="bbc6a-154">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="bbc6a-155">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="bbc6a-155">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="bbc6a-156">How do Azure Active Directory admins add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="bbc6a-156">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="bbc6a-157">How do information workers add B2B collaboration users?</span><span class="sxs-lookup"><span data-stu-id="bbc6a-157">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="bbc6a-158">The elements of the B2B collaboration invitation email</span><span class="sxs-lookup"><span data-stu-id="bbc6a-158">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="bbc6a-159">B2B collaboration invitation redemption</span><span class="sxs-lookup"><span data-stu-id="bbc6a-159">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="bbc6a-160">Azure AD B2B collaboration licensing</span><span class="sxs-lookup"><span data-stu-id="bbc6a-160">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="bbc6a-161">Troubleshooting Azure Active Directory B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="bbc6a-161">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="bbc6a-162">Azure Active Directory B2B collaboration frequently-asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="bbc6a-162">Azure Active Directory B2B collaboration frequently-asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="bbc6a-163">Azure Active Directory B2B collaboration API and customization</span><span class="sxs-lookup"><span data-stu-id="bbc6a-163">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="bbc6a-164">Add B2B collaboration users without an invitation</span><span class="sxs-lookup"><span data-stu-id="bbc6a-164">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="bbc6a-165">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbc6a-165">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
