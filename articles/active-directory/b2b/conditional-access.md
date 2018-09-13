---
title: Conditional access for Azure Active Directory B2B collaboration users | Microsoft Docs
description: Azure Active Directory B2B collaboration supports multi-factor authentication (MFA) for selective access to your corporate applications
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 09/11/2017
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: 8e8e73b9206cf2134e96e609dfe5558c54e4289c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858030"
---
# <a name="conditional-access-for-b2b-collaboration-users"></a><span data-ttu-id="f3192-103">Conditional access for B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="f3192-103">Conditional access for B2B collaboration users</span></span>

## <a name="multi-factor-authentication-for-b2b-users"></a><span data-ttu-id="f3192-104">Multi-factor authentication for B2B users</span><span class="sxs-lookup"><span data-stu-id="f3192-104">Multi-factor authentication for B2B users</span></span>
<span data-ttu-id="f3192-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span><span class="sxs-lookup"><span data-stu-id="f3192-105">With Azure AD B2B collaboration, organizations can enforce multi-factor authentication (MFA) policies for B2B users.</span></span> <span data-ttu-id="f3192-106">These policies can be enforced at the tenant, app, or individual user level, the same way that they are enabled for full-time employees and members of the organization.</span><span class="sxs-lookup"><span data-stu-id="f3192-106">These policies can be enforced at the tenant, app, or individual user level, the same way that they are enabled for full-time employees and members of the organization.</span></span> <span data-ttu-id="f3192-107">MFA policies are enforced at the resource organization.</span><span class="sxs-lookup"><span data-stu-id="f3192-107">MFA policies are enforced at the resource organization.</span></span>

<span data-ttu-id="f3192-108">Example:</span><span class="sxs-lookup"><span data-stu-id="f3192-108">Example:</span></span>
1. <span data-ttu-id="f3192-109">Admin or information worker in Company A invites user from company B to an application *Foo* in company A.</span><span class="sxs-lookup"><span data-stu-id="f3192-109">Admin or information worker in Company A invites user from company B to an application *Foo* in company A.</span></span>
2. <span data-ttu-id="f3192-110">Application *Foo* in company A is configured to require MFA on access.</span><span class="sxs-lookup"><span data-stu-id="f3192-110">Application *Foo* in company A is configured to require MFA on access.</span></span>
3. <span data-ttu-id="f3192-111">When the user from company B attempts to access app *Foo* in the company A tenant, they are asked to complete an MFA challenge.</span><span class="sxs-lookup"><span data-stu-id="f3192-111">When the user from company B attempts to access app *Foo* in the company A tenant, they are asked to complete an MFA challenge.</span></span>
4. <span data-ttu-id="f3192-112">The user can set up their MFA with company A, and chooses their MFA option.</span><span class="sxs-lookup"><span data-stu-id="f3192-112">The user can set up their MFA with company A, and chooses their MFA option.</span></span>
5. <span data-ttu-id="f3192-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span><span class="sxs-lookup"><span data-stu-id="f3192-113">This scenario works for any identity (Azure AD or MSA, for example, if users in Company B authenticate using social ID)</span></span>
6. <span data-ttu-id="f3192-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span><span class="sxs-lookup"><span data-stu-id="f3192-114">Company A must have sufficient Premium Azure AD licenses that support MFA.</span></span> <span data-ttu-id="f3192-115">The user from company B consumes this license from company A.</span><span class="sxs-lookup"><span data-stu-id="f3192-115">The user from company B consumes this license from company A.</span></span>

<span data-ttu-id="f3192-116">The inviting tenancy is always responsible for MFA for users from the partner organization, even if the partner organization has MFA capabilities.</span><span class="sxs-lookup"><span data-stu-id="f3192-116">The inviting tenancy is always responsible for MFA for users from the partner organization, even if the partner organization has MFA capabilities.</span></span>

### <a name="setting-up-mfa-for-b2b-collaboration-users"></a><span data-ttu-id="f3192-117">Setting up MFA for B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="f3192-117">Setting up MFA for B2B collaboration users</span></span>
<span data-ttu-id="f3192-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span><span class="sxs-lookup"><span data-stu-id="f3192-118">To discover how easy it is to set up MFA for B2B collaboration users, see how in the following video:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/b2b-conditional-access-setup/Player]

### <a name="b2b-users-mfa-experience-for-offer-redemption"></a><span data-ttu-id="f3192-119">B2B users MFA experience for offer redemption</span><span class="sxs-lookup"><span data-stu-id="f3192-119">B2B users MFA experience for offer redemption</span></span>
<span data-ttu-id="f3192-120">Check out the following animation to see the redemption experience:</span><span class="sxs-lookup"><span data-stu-id="f3192-120">Check out the following animation to see the redemption experience:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure/MFA-redemption/Player]

### <a name="mfa-reset-for-b2b-collaboration-users"></a><span data-ttu-id="f3192-121">MFA reset for B2B collaboration users</span><span class="sxs-lookup"><span data-stu-id="f3192-121">MFA reset for B2B collaboration users</span></span>
<span data-ttu-id="f3192-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets:</span><span class="sxs-lookup"><span data-stu-id="f3192-122">Currently, the admin can require B2B collaboration users to proof up again only by using the following PowerShell cmdlets:</span></span>

1. <span data-ttu-id="f3192-123">Connect to Azure AD</span><span class="sxs-lookup"><span data-stu-id="f3192-123">Connect to Azure AD</span></span>

  ```
  $cred = Get-Credential
  Connect-MsolService -Credential $cred
  ```
2. <span data-ttu-id="f3192-124">Get all users with proof up methods</span><span class="sxs-lookup"><span data-stu-id="f3192-124">Get all users with proof up methods</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```
  <span data-ttu-id="f3192-125">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="f3192-125">Here is an example:</span></span>

  ```
  Get-MsolUser | where { $_.StrongAuthenticationMethods} | select UserPrincipalName, @{n="Methods";e={($_.StrongAuthenticationMethods).MethodType}}
  ```

3. <span data-ttu-id="f3192-126">Reset the MFA method for a specific user to require the B2B collaboration user to set proof-up methods again.</span><span class="sxs-lookup"><span data-stu-id="f3192-126">Reset the MFA method for a specific user to require the B2B collaboration user to set proof-up methods again.</span></span> <span data-ttu-id="f3192-127">Example:</span><span class="sxs-lookup"><span data-stu-id="f3192-127">Example:</span></span>

  ```
  Reset-MsolStrongAuthenticationMethodByUpn -UserPrincipalName gsamoogle_gmail.com#EXT#@ WoodGroveAzureAD.onmicrosoft.com
  ```

### <a name="why-do-we-perform-mfa-at-the-resource-tenancy"></a><span data-ttu-id="f3192-128">Why do we perform MFA at the resource tenancy?</span><span class="sxs-lookup"><span data-stu-id="f3192-128">Why do we perform MFA at the resource tenancy?</span></span>

<span data-ttu-id="f3192-129">In the current release, MFA is always in the resource tenancy, for reasons of predictability.</span><span class="sxs-lookup"><span data-stu-id="f3192-129">In the current release, MFA is always in the resource tenancy, for reasons of predictability.</span></span> <span data-ttu-id="f3192-130">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span><span class="sxs-lookup"><span data-stu-id="f3192-130">For example, let’s say a Contoso user (Sally) is invited to Fabrikam and Fabrikam has enabled MFA for B2B users.</span></span>

<span data-ttu-id="f3192-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at the Contoso MFA claim in the token, we might see the following issue:</span><span class="sxs-lookup"><span data-stu-id="f3192-131">If Contoso has MFA policy enabled for App1 but not App2, then if we look at the Contoso MFA claim in the token, we might see the following issue:</span></span>

* <span data-ttu-id="f3192-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="f3192-132">Day 1: A user has MFA in Contoso and is accessing App1, then no additional MFA prompt is shown in Fabrikam.</span></span>

* <span data-ttu-id="f3192-133">Day 2: The user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span><span class="sxs-lookup"><span data-stu-id="f3192-133">Day 2: The user has accessed App 2 in Contoso, so now when accessing Fabrikam, they must register for MFA there.</span></span>

<span data-ttu-id="f3192-134">This process can be confusing and could lead to drop in sign-in completions.</span><span class="sxs-lookup"><span data-stu-id="f3192-134">This process can be confusing and could lead to drop in sign-in completions.</span></span>

<span data-ttu-id="f3192-135">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span><span class="sxs-lookup"><span data-stu-id="f3192-135">Moreover, even if Contoso has MFA capability, it is not always the case the Fabrikam would trust the Contoso MFA policy.</span></span>

<span data-ttu-id="f3192-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span><span class="sxs-lookup"><span data-stu-id="f3192-136">Finally, resource tenant MFA also works for MSAs and social IDs and for partner orgs that do not have MFA set up.</span></span>

<span data-ttu-id="f3192-137">Therefore, the recommendation for MFA for B2B users is to always require MFA in the inviting tenant.</span><span class="sxs-lookup"><span data-stu-id="f3192-137">Therefore, the recommendation for MFA for B2B users is to always require MFA in the inviting tenant.</span></span> <span data-ttu-id="f3192-138">This requirement could lead to double MFA in some cases, but whenever accessing the inviting tenant, the end-users experience is predictable: Sally must register for MFA with the inviting tenant.</span><span class="sxs-lookup"><span data-stu-id="f3192-138">This requirement could lead to double MFA in some cases, but whenever accessing the inviting tenant, the end-users experience is predictable: Sally must register for MFA with the inviting tenant.</span></span>

### <a name="device-based-location-based-and-risk-based-conditional-access-for-b2b-users"></a><span data-ttu-id="f3192-139">Device-based, location-based, and risk-based conditional access for B2B users</span><span class="sxs-lookup"><span data-stu-id="f3192-139">Device-based, location-based, and risk-based conditional access for B2B users</span></span>

<span data-ttu-id="f3192-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with the Contoso device policies.</span><span class="sxs-lookup"><span data-stu-id="f3192-140">When Contoso enables device-based conditional access policies for their corporate data, access is prevented from devices that are not managed by Contoso and not compliant with the Contoso device policies.</span></span>

<span data-ttu-id="f3192-141">If the B2B user’s device isn't managed by Contoso, access of B2B users from the partner organizations is blocked in whatever context these policies are enforced.</span><span class="sxs-lookup"><span data-stu-id="f3192-141">If the B2B user’s device isn't managed by Contoso, access of B2B users from the partner organizations is blocked in whatever context these policies are enforced.</span></span> <span data-ttu-id="f3192-142">However, Contoso can create exclusion lists containing specific partner users to exclude them from the device-based conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="f3192-142">However, Contoso can create exclusion lists containing specific partner users to exclude them from the device-based conditional access policy.</span></span>

#### <a name="location-based-conditional-access-for-b2b"></a><span data-ttu-id="f3192-143">Location-based conditional access for B2B</span><span class="sxs-lookup"><span data-stu-id="f3192-143">Location-based conditional access for B2B</span></span>

<span data-ttu-id="f3192-144">Location-based conditional access policies can be enforced for B2B users if the inviting organization is able to create a trusted IP address range that defines their partner organizations.</span><span class="sxs-lookup"><span data-stu-id="f3192-144">Location-based conditional access policies can be enforced for B2B users if the inviting organization is able to create a trusted IP address range that defines their partner organizations.</span></span>

#### <a name="risk-based-conditional-access-for-b2b"></a><span data-ttu-id="f3192-145">Risk-based conditional access for B2B</span><span class="sxs-lookup"><span data-stu-id="f3192-145">Risk-based conditional access for B2B</span></span>

<span data-ttu-id="f3192-146">Currently, risk-based sign-in policies cannot be applied to B2B users because the risk evaluation is performed at the B2B user’s home organization.</span><span class="sxs-lookup"><span data-stu-id="f3192-146">Currently, risk-based sign-in policies cannot be applied to B2B users because the risk evaluation is performed at the B2B user’s home organization.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3192-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="f3192-147">Next steps</span></span>

<span data-ttu-id="f3192-148">See the following articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="f3192-148">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="f3192-149">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="f3192-149">What is Azure AD B2B collaboration?</span></span>](what-is-b2b.md)
* [<span data-ttu-id="f3192-150">Azure AD B2B collaboration licensing</span><span class="sxs-lookup"><span data-stu-id="f3192-150">Azure AD B2B collaboration licensing</span></span>](licensing-guidance.md)
* [<span data-ttu-id="f3192-151">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="f3192-151">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](faq.md)
