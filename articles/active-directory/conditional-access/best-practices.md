---
title: Best practices for conditional access in Azure Active Directory  | Microsoft Docs
description: Learn about things you should know and what it is you should avoid doing when configuring conditional access policies.
services: active-directory
keywords: conditional access to apps, conditional access with Azure AD, secure access to company resources, conditional access policies
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 8c1d978f-e80b-420e-853a-8bbddc4bcdad
ms.service: active-directory
ms.component: conditional-access
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/23/2018
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 4e9f5a9318db813b1a0f16d3599f74fd98e53ffc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965808"
---
# <a name="best-practices-for-conditional-access-in-azure-active-directory"></a><span data-ttu-id="94be6-104">Best practices for conditional access in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="94be6-104">Best practices for conditional access in Azure Active Directory</span></span>

<span data-ttu-id="94be6-105">With [Azure Active Directory (Azure AD) conditional access](../active-directory-conditional-access-azure-portal.md), you can control how authorized users access your cloud apps.</span><span class="sxs-lookup"><span data-stu-id="94be6-105">With [Azure Active Directory (Azure AD) conditional access](../active-directory-conditional-access-azure-portal.md), you can control how authorized users access your cloud apps.</span></span> <span data-ttu-id="94be6-106">This article provides you with information about:</span><span class="sxs-lookup"><span data-stu-id="94be6-106">This article provides you with information about:</span></span>

- <span data-ttu-id="94be6-107">Things you should know</span><span class="sxs-lookup"><span data-stu-id="94be6-107">Things you should know</span></span> 
- <span data-ttu-id="94be6-108">What it is you should avoid doing when configuring conditional access policies.</span><span class="sxs-lookup"><span data-stu-id="94be6-108">What it is you should avoid doing when configuring conditional access policies.</span></span> 

<span data-ttu-id="94be6-109">This article assumes that you familiar the concepts and the terminology outlined in [What is conditional access in Azure Active Directory?](../active-directory-conditional-access-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="94be6-109">This article assumes that you familiar the concepts and the terminology outlined in [What is conditional access in Azure Active Directory?](../active-directory-conditional-access-azure-portal.md)</span></span>



## <a name="whats-required-to-make-a-policy-work"></a><span data-ttu-id="94be6-110">What’s required to make a policy work?</span><span class="sxs-lookup"><span data-stu-id="94be6-110">What’s required to make a policy work?</span></span>

<span data-ttu-id="94be6-111">When you create a new policy, there are no users, groups, apps, or access controls selected.</span><span class="sxs-lookup"><span data-stu-id="94be6-111">When you create a new policy, there are no users, groups, apps, or access controls selected.</span></span>

![Cloud apps](./media/best-practices/02.png)


<span data-ttu-id="94be6-113">To make your policy work, you must configure:</span><span class="sxs-lookup"><span data-stu-id="94be6-113">To make your policy work, you must configure:</span></span>


|<span data-ttu-id="94be6-114">What</span><span class="sxs-lookup"><span data-stu-id="94be6-114">What</span></span>           | <span data-ttu-id="94be6-115">How</span><span class="sxs-lookup"><span data-stu-id="94be6-115">How</span></span>                                  | <span data-ttu-id="94be6-116">Why</span><span class="sxs-lookup"><span data-stu-id="94be6-116">Why</span></span>|
|:--            | :--                                  | :-- |
|<span data-ttu-id="94be6-117">**Cloud apps**</span><span class="sxs-lookup"><span data-stu-id="94be6-117">**Cloud apps**</span></span> |<span data-ttu-id="94be6-118">You need to select one or more apps.</span><span class="sxs-lookup"><span data-stu-id="94be6-118">You need to select one or more apps.</span></span>  | <span data-ttu-id="94be6-119">The goal of a conditional access policy is to enable you to control how authorized users can access cloud apps.</span><span class="sxs-lookup"><span data-stu-id="94be6-119">The goal of a conditional access policy is to enable you to control how authorized users can access cloud apps.</span></span>|
| <span data-ttu-id="94be6-120">**Users and groups**</span><span class="sxs-lookup"><span data-stu-id="94be6-120">**Users and groups**</span></span> | <span data-ttu-id="94be6-121">You need to select at least one user or group that is authorized to access your selected cloud apps.</span><span class="sxs-lookup"><span data-stu-id="94be6-121">You need to select at least one user or group that is authorized to access your selected cloud apps.</span></span> | <span data-ttu-id="94be6-122">A conditional access policy that has no users and groups assigned, is never triggered.</span><span class="sxs-lookup"><span data-stu-id="94be6-122">A conditional access policy that has no users and groups assigned, is never triggered.</span></span> |
| <span data-ttu-id="94be6-123">**Access controls**</span><span class="sxs-lookup"><span data-stu-id="94be6-123">**Access controls**</span></span> | <span data-ttu-id="94be6-124">You need to select at least one access control.</span><span class="sxs-lookup"><span data-stu-id="94be6-124">You need to select at least one access control.</span></span> | <span data-ttu-id="94be6-125">If your conditions are satisfied, your policy processor needs to know what to do.</span><span class="sxs-lookup"><span data-stu-id="94be6-125">If your conditions are satisfied, your policy processor needs to know what to do.</span></span>|




## <a name="what-you-should-know"></a><span data-ttu-id="94be6-126">What you should know</span><span class="sxs-lookup"><span data-stu-id="94be6-126">What you should know</span></span>

### <a name="how-are-assignments-evaluated"></a><span data-ttu-id="94be6-127">How are assignments evaluated?</span><span class="sxs-lookup"><span data-stu-id="94be6-127">How are assignments evaluated?</span></span>

<span data-ttu-id="94be6-128">All assignments are logically **ANDed**.</span><span class="sxs-lookup"><span data-stu-id="94be6-128">All assignments are logically **ANDed**.</span></span> <span data-ttu-id="94be6-129">If you have more than one assignment configured, all assignments must be satisfied to trigger a policy.</span><span class="sxs-lookup"><span data-stu-id="94be6-129">If you have more than one assignment configured, all assignments must be satisfied to trigger a policy.</span></span>  

<span data-ttu-id="94be6-130">If you need to configure a location condition that applies to all connections made from outside your organization's network:</span><span class="sxs-lookup"><span data-stu-id="94be6-130">If you need to configure a location condition that applies to all connections made from outside your organization's network:</span></span>

- <span data-ttu-id="94be6-131">Include **All locations**</span><span class="sxs-lookup"><span data-stu-id="94be6-131">Include **All locations**</span></span>
- <span data-ttu-id="94be6-132">Exclude **All trusted IPs**</span><span class="sxs-lookup"><span data-stu-id="94be6-132">Exclude **All trusted IPs**</span></span>


### <a name="what-to-do-if-you-are-locked-out-of-the-azure-ad-admin-portal"></a><span data-ttu-id="94be6-133">What to do if you are locked out of the Azure AD admin portal?</span><span class="sxs-lookup"><span data-stu-id="94be6-133">What to do if you are locked out of the Azure AD admin portal?</span></span>

<span data-ttu-id="94be6-134">If you are locked out of the Azure AD portal due to an incorrect setting in a conditional access policy:</span><span class="sxs-lookup"><span data-stu-id="94be6-134">If you are locked out of the Azure AD portal due to an incorrect setting in a conditional access policy:</span></span>

- <span data-ttu-id="94be6-135">Verify whether there are other administrators in your organization that are not blocked yet.</span><span class="sxs-lookup"><span data-stu-id="94be6-135">Verify whether there are other administrators in your organization that are not blocked yet.</span></span> <span data-ttu-id="94be6-136">An administrator with access to the Azure portal can disable the policy that is impacting your sign in.</span><span class="sxs-lookup"><span data-stu-id="94be6-136">An administrator with access to the Azure portal can disable the policy that is impacting your sign in.</span></span> 

- <span data-ttu-id="94be6-137">If none of the administrators in your organization can update the policy, you need to submit a support request.</span><span class="sxs-lookup"><span data-stu-id="94be6-137">If none of the administrators in your organization can update the policy, you need to submit a support request.</span></span> <span data-ttu-id="94be6-138">Microsoft support can review and update conditional access policies that are preventing access.</span><span class="sxs-lookup"><span data-stu-id="94be6-138">Microsoft support can review and update conditional access policies that are preventing access.</span></span>


### <a name="what-happens-if-you-have-policies-in-the-azure-classic-portal-and-azure-portal-configured"></a><span data-ttu-id="94be6-139">What happens if you have policies in the Azure classic portal and Azure portal configured?</span><span class="sxs-lookup"><span data-stu-id="94be6-139">What happens if you have policies in the Azure classic portal and Azure portal configured?</span></span>  

<span data-ttu-id="94be6-140">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span><span class="sxs-lookup"><span data-stu-id="94be6-140">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-you-have-policies-in-the-intune-silverlight-portal-and-the-azure-portal"></a><span data-ttu-id="94be6-141">What happens if you have policies in the Intune Silverlight portal and the Azure portal?</span><span class="sxs-lookup"><span data-stu-id="94be6-141">What happens if you have policies in the Intune Silverlight portal and the Azure portal?</span></span>

<span data-ttu-id="94be6-142">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span><span class="sxs-lookup"><span data-stu-id="94be6-142">Both policies are enforced by Azure Active Directory and the user gets access only when all requirements are met.</span></span>

### <a name="what-happens-if-i-have-multiple-policies-for-the-same-user-configured"></a><span data-ttu-id="94be6-143">What happens if I have multiple policies for the same user configured?</span><span class="sxs-lookup"><span data-stu-id="94be6-143">What happens if I have multiple policies for the same user configured?</span></span>  

<span data-ttu-id="94be6-144">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access to the user.</span><span class="sxs-lookup"><span data-stu-id="94be6-144">For every sign-in, Azure Active Directory evaluates all policies and ensures that all requirements are met before granted access to the user.</span></span> <span data-ttu-id="94be6-145">Block access trumps all other configuration settings.</span><span class="sxs-lookup"><span data-stu-id="94be6-145">Block access trumps all other configuration settings.</span></span> 


### <a name="does-conditional-access-work-with-exchange-activesync"></a><span data-ttu-id="94be6-146">Does conditional access work with Exchange ActiveSync?</span><span class="sxs-lookup"><span data-stu-id="94be6-146">Does conditional access work with Exchange ActiveSync?</span></span>

<span data-ttu-id="94be6-147">Yes, you can use Exchange ActiveSync in a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="94be6-147">Yes, you can use Exchange ActiveSync in a conditional access policy.</span></span>






## <a name="what-you-should-avoid-doing"></a><span data-ttu-id="94be6-148">What you should avoid doing</span><span class="sxs-lookup"><span data-stu-id="94be6-148">What you should avoid doing</span></span>

<span data-ttu-id="94be6-149">The conditional access framework provides you with a great configuration flexibility.</span><span class="sxs-lookup"><span data-stu-id="94be6-149">The conditional access framework provides you with a great configuration flexibility.</span></span> <span data-ttu-id="94be6-150">However, great flexibility  also means that you should carefully review each configuration policy before releasing it to avoid undesirable results.</span><span class="sxs-lookup"><span data-stu-id="94be6-150">However, great flexibility  also means that you should carefully review each configuration policy before releasing it to avoid undesirable results.</span></span> <span data-ttu-id="94be6-151">In this context, you should pay special attention to assignments affecting complete sets such as **all users / groups / cloud apps**.</span><span class="sxs-lookup"><span data-stu-id="94be6-151">In this context, you should pay special attention to assignments affecting complete sets such as **all users / groups / cloud apps**.</span></span>

<span data-ttu-id="94be6-152">In your environment, you should avoid the following configurations:</span><span class="sxs-lookup"><span data-stu-id="94be6-152">In your environment, you should avoid the following configurations:</span></span>


<span data-ttu-id="94be6-153">**For all users, all cloud apps:**</span><span class="sxs-lookup"><span data-stu-id="94be6-153">**For all users, all cloud apps:**</span></span>

- <span data-ttu-id="94be6-154">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span><span class="sxs-lookup"><span data-stu-id="94be6-154">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>

- <span data-ttu-id="94be6-155">**Require compliant device** - For users that have not enrolled their devices yet, this policy blocks all access including access to the Intune portal.</span><span class="sxs-lookup"><span data-stu-id="94be6-155">**Require compliant device** - For users that have not enrolled their devices yet, this policy blocks all access including access to the Intune portal.</span></span> <span data-ttu-id="94be6-156">If you are an administrator without an enrolled device, this policy blocks you from getting back into the Azure portal to change the policy.</span><span class="sxs-lookup"><span data-stu-id="94be6-156">If you are an administrator without an enrolled device, this policy blocks you from getting back into the Azure portal to change the policy.</span></span>

- <span data-ttu-id="94be6-157">**Require domain join** - This policy block access has also the potential to block access for all users in your organization if you don't have a domain-joined device yet.</span><span class="sxs-lookup"><span data-stu-id="94be6-157">**Require domain join** - This policy block access has also the potential to block access for all users in your organization if you don't have a domain-joined device yet.</span></span>


<span data-ttu-id="94be6-158">**For all users, all cloud apps, all device platforms:**</span><span class="sxs-lookup"><span data-stu-id="94be6-158">**For all users, all cloud apps, all device platforms:**</span></span>

- <span data-ttu-id="94be6-159">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span><span class="sxs-lookup"><span data-stu-id="94be6-159">**Block access** - This configuration blocks your entire organization, which is definitely not a good idea.</span></span>


## <a name="how-should-you-deploy-a-new-policy"></a><span data-ttu-id="94be6-160">How should you deploy a new policy?</span><span class="sxs-lookup"><span data-stu-id="94be6-160">How should you deploy a new policy?</span></span>

<span data-ttu-id="94be6-161">As a first step, you should evaluate your policy using the [what if tool](what-if-tool.md).</span><span class="sxs-lookup"><span data-stu-id="94be6-161">As a first step, you should evaluate your policy using the [what if tool](what-if-tool.md).</span></span>

<span data-ttu-id="94be6-162">When you are ready to deploy a new policy into your environment, you should do this in phases:</span><span class="sxs-lookup"><span data-stu-id="94be6-162">When you are ready to deploy a new policy into your environment, you should do this in phases:</span></span>

1. <span data-ttu-id="94be6-163">Apply a policy to a small set of users and verify it behaves as expected.</span><span class="sxs-lookup"><span data-stu-id="94be6-163">Apply a policy to a small set of users and verify it behaves as expected.</span></span> 

2.  <span data-ttu-id="94be6-164">When you expand a policy to include more users, continue to exclude all administrators from the policy.</span><span class="sxs-lookup"><span data-stu-id="94be6-164">When you expand a policy to include more users, continue to exclude all administrators from the policy.</span></span> <span data-ttu-id="94be6-165">This ensures that administrators still have access and can update a policy if a change is required.</span><span class="sxs-lookup"><span data-stu-id="94be6-165">This ensures that administrators still have access and can update a policy if a change is required.</span></span>

3. <span data-ttu-id="94be6-166">Apply a policy to all users only if this is really required.</span><span class="sxs-lookup"><span data-stu-id="94be6-166">Apply a policy to all users only if this is really required.</span></span> 

<span data-ttu-id="94be6-167">As a best practice, create a user account that is:</span><span class="sxs-lookup"><span data-stu-id="94be6-167">As a best practice, create a user account that is:</span></span>

- <span data-ttu-id="94be6-168">Dedicated to policy administration</span><span class="sxs-lookup"><span data-stu-id="94be6-168">Dedicated to policy administration</span></span> 
- <span data-ttu-id="94be6-169">Excluded from all your policies</span><span class="sxs-lookup"><span data-stu-id="94be6-169">Excluded from all your policies</span></span>


## <a name="policy-migration"></a><span data-ttu-id="94be6-170">Policy migration</span><span class="sxs-lookup"><span data-stu-id="94be6-170">Policy migration</span></span>

<span data-ttu-id="94be6-171">Consider migrating the policies you have not created in the Azure portal because:</span><span class="sxs-lookup"><span data-stu-id="94be6-171">Consider migrating the policies you have not created in the Azure portal because:</span></span>

- <span data-ttu-id="94be6-172">You can now address scenarios you could not handle before.</span><span class="sxs-lookup"><span data-stu-id="94be6-172">You can now address scenarios you could not handle before.</span></span>

- <span data-ttu-id="94be6-173">You can reduce the number of policies you have to manage by consolidating them.</span><span class="sxs-lookup"><span data-stu-id="94be6-173">You can reduce the number of policies you have to manage by consolidating them.</span></span>   

- <span data-ttu-id="94be6-174">You can manage all your conditional access policies in one central location.</span><span class="sxs-lookup"><span data-stu-id="94be6-174">You can manage all your conditional access policies in one central location.</span></span>

- <span data-ttu-id="94be6-175">The Azure classic portal has been retired.</span><span class="sxs-lookup"><span data-stu-id="94be6-175">The Azure classic portal has been retired.</span></span>   


<span data-ttu-id="94be6-176">For more information, see [Migrate classic policies in the Azure portal](policy-migration.md).</span><span class="sxs-lookup"><span data-stu-id="94be6-176">For more information, see [Migrate classic policies in the Azure portal](policy-migration.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="94be6-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="94be6-177">Next steps</span></span>

<span data-ttu-id="94be6-178">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span><span class="sxs-lookup"><span data-stu-id="94be6-178">If you want to know how to configure a conditional access policy, see [Require MFA for specific apps with Azure Active Directory conditional access](app-based-mfa.md).</span></span>
