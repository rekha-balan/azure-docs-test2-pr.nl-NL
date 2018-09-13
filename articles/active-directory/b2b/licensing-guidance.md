---
title: Azure Active Directory B2B collaboration licensing guidance | Microsoft Docs
description: Azure Active Directory B2B collaboration does not require paid Azure AD licenses, but you can also get paid features for B2B guest users
services: active-directory
ms.service: active-directory
ms.component: B2B
ms.topic: article
ms.date: 08/09/2017
ms.author: mimart
author: msmimart
manager: mtillman
ms.reviewer: sasubram
ms.openlocfilehash: 2050952eb924e1eee5e6d7d6312d9cd02f475d10
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969099"
---
# <a name="azure-active-directory-b2b-collaboration-licensing-guidance"></a><span data-ttu-id="60087-103">Azure Active Directory B2B collaboration licensing guidance</span><span class="sxs-lookup"><span data-stu-id="60087-103">Azure Active Directory B2B collaboration licensing guidance</span></span>

<span data-ttu-id="60087-104">You can use Azure AD B2B collaboration capabilities to invite guest users into your Azure AD tenant to allow them to access Azure AD services and other resources in your organization.</span><span class="sxs-lookup"><span data-stu-id="60087-104">You can use Azure AD B2B collaboration capabilities to invite guest users into your Azure AD tenant to allow them to access Azure AD services and other resources in your organization.</span></span> <span data-ttu-id="60087-105">If you want to provide access to paid Azure AD features, B2B collaboration guest users must be licensed with appropriate Azure AD licenses.</span><span class="sxs-lookup"><span data-stu-id="60087-105">If you want to provide access to paid Azure AD features, B2B collaboration guest users must be licensed with appropriate Azure AD licenses.</span></span> 

<span data-ttu-id="60087-106">Specifically:</span><span class="sxs-lookup"><span data-stu-id="60087-106">Specifically:</span></span>
* <span data-ttu-id="60087-107">Azure AD Free capabilities are available for guest users without additional licensing.</span><span class="sxs-lookup"><span data-stu-id="60087-107">Azure AD Free capabilities are available for guest users without additional licensing.</span></span>
* <span data-ttu-id="60087-108">If you want to provide access to paid Azure AD features to B2B users, you must have enough licenses to support those B2B guest users.</span><span class="sxs-lookup"><span data-stu-id="60087-108">If you want to provide access to paid Azure AD features to B2B users, you must have enough licenses to support those B2B guest users.</span></span>
* <span data-ttu-id="60087-109">An inviting tenant with an Azure AD paid license has B2B collaboration use rights to an additional five B2B guest users invited to the tenant.</span><span class="sxs-lookup"><span data-stu-id="60087-109">An inviting tenant with an Azure AD paid license has B2B collaboration use rights to an additional five B2B guest users invited to the tenant.</span></span>
* <span data-ttu-id="60087-110">The customer who owns the inviting tenant must be the one to determine how many B2B collaboration users need paid Azure AD capabilities.</span><span class="sxs-lookup"><span data-stu-id="60087-110">The customer who owns the inviting tenant must be the one to determine how many B2B collaboration users need paid Azure AD capabilities.</span></span> <span data-ttu-id="60087-111">Depending on the paid Azure AD features you want for your guest users, you must have enough Azure AD paid licenses to cover B2B collaboration users in the same 5:1 ratio.</span><span class="sxs-lookup"><span data-stu-id="60087-111">Depending on the paid Azure AD features you want for your guest users, you must have enough Azure AD paid licenses to cover B2B collaboration users in the same 5:1 ratio.</span></span>

<span data-ttu-id="60087-112">A B2B collaboration guest user is added as a user from a partner company, not an employee of your organization or an employee of a different business in your conglomerate.</span><span class="sxs-lookup"><span data-stu-id="60087-112">A B2B collaboration guest user is added as a user from a partner company, not an employee of your organization or an employee of a different business in your conglomerate.</span></span> <span data-ttu-id="60087-113">A B2B guest user can sign in with external credentials or credentials owned by your organization as described in this article.</span><span class="sxs-lookup"><span data-stu-id="60087-113">A B2B guest user can sign in with external credentials or credentials owned by your organization as described in this article.</span></span> 

<span data-ttu-id="60087-114">In other words, B2B licensing is set not by how the user authenticates but rather by the relationship of the user to your organization.</span><span class="sxs-lookup"><span data-stu-id="60087-114">In other words, B2B licensing is set not by how the user authenticates but rather by the relationship of the user to your organization.</span></span> <span data-ttu-id="60087-115">If these users are not partners, they are treated differently in licensing terms.</span><span class="sxs-lookup"><span data-stu-id="60087-115">If these users are not partners, they are treated differently in licensing terms.</span></span> <span data-ttu-id="60087-116">They are not considered to be a B2B collaboration user for licensing purposes even if their UserType is marked as “Guest.”</span><span class="sxs-lookup"><span data-stu-id="60087-116">They are not considered to be a B2B collaboration user for licensing purposes even if their UserType is marked as “Guest.”</span></span> <span data-ttu-id="60087-117">They should be licensed normally, at one license per user.</span><span class="sxs-lookup"><span data-stu-id="60087-117">They should be licensed normally, at one license per user.</span></span> <span data-ttu-id="60087-118">These users include:</span><span class="sxs-lookup"><span data-stu-id="60087-118">These users include:</span></span>
* <span data-ttu-id="60087-119">Your employees</span><span class="sxs-lookup"><span data-stu-id="60087-119">Your employees</span></span>
* <span data-ttu-id="60087-120">Staff signing in using external identities</span><span class="sxs-lookup"><span data-stu-id="60087-120">Staff signing in using external identities</span></span>
* <span data-ttu-id="60087-121">An employee of a different business in your conglomerate</span><span class="sxs-lookup"><span data-stu-id="60087-121">An employee of a different business in your conglomerate</span></span>


## <a name="licensing-examples"></a><span data-ttu-id="60087-122">Licensing examples</span><span class="sxs-lookup"><span data-stu-id="60087-122">Licensing examples</span></span>
- <span data-ttu-id="60087-123">A customer wants to invite 100 B2B collaboration users to its Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="60087-123">A customer wants to invite 100 B2B collaboration users to its Azure AD tenant.</span></span> <span data-ttu-id="60087-124">The customer assigns access management and provisioning for all users, but 50 users also require MFA and conditional access.</span><span class="sxs-lookup"><span data-stu-id="60087-124">The customer assigns access management and provisioning for all users, but 50 users also require MFA and conditional access.</span></span> <span data-ttu-id="60087-125">This customer must purchase 10 Azure AD Basic licenses and 10 Azure AD Premium P1 licenses to cover these B2B users correctly.</span><span class="sxs-lookup"><span data-stu-id="60087-125">This customer must purchase 10 Azure AD Basic licenses and 10 Azure AD Premium P1 licenses to cover these B2B users correctly.</span></span> <span data-ttu-id="60087-126">If the customer plans to use Identity Protection features with B2B users, they must have Azure AD Premium P2 licenses to cover the invited users in the same 5:1 ratio.</span><span class="sxs-lookup"><span data-stu-id="60087-126">If the customer plans to use Identity Protection features with B2B users, they must have Azure AD Premium P2 licenses to cover the invited users in the same 5:1 ratio.</span></span>
- <span data-ttu-id="60087-127">A customer has 10 employees who are all currently licensed with Azure AD Premium P1.</span><span class="sxs-lookup"><span data-stu-id="60087-127">A customer has 10 employees who are all currently licensed with Azure AD Premium P1.</span></span> <span data-ttu-id="60087-128">They now want to invite 60 B2B users who all require multi-factor authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="60087-128">They now want to invite 60 B2B users who all require multi-factor authentication (MFA).</span></span> <span data-ttu-id="60087-129">Under the 5:1 licensing rule, the customer must have at least 12 Azure AD Premium P1 licenses to cover all 60 B2B collaboration users.</span><span class="sxs-lookup"><span data-stu-id="60087-129">Under the 5:1 licensing rule, the customer must have at least 12 Azure AD Premium P1 licenses to cover all 60 B2B collaboration users.</span></span> <span data-ttu-id="60087-130">Because they already have 10 Premium P1 licenses for their 10 employees, they have rights to invite 50 B2B users with Premium P1 features like MFA.</span><span class="sxs-lookup"><span data-stu-id="60087-130">Because they already have 10 Premium P1 licenses for their 10 employees, they have rights to invite 50 B2B users with Premium P1 features like MFA.</span></span> <span data-ttu-id="60087-131">In this example, then, they must purchase 2 additional Premium P1 licenses to cover the remaining 10 B2B collaboration users.</span><span class="sxs-lookup"><span data-stu-id="60087-131">In this example, then, they must purchase 2 additional Premium P1 licenses to cover the remaining 10 B2B collaboration users.</span></span>

> [!NOTE]
> <span data-ttu-id="60087-132">There is no way yet to assign licenses directly to the B2B users to enable these B2B collaboration user rights.</span><span class="sxs-lookup"><span data-stu-id="60087-132">There is no way yet to assign licenses directly to the B2B users to enable these B2B collaboration user rights.</span></span>

<span data-ttu-id="60087-133">The customer who owns the inviting tenant must be the one to determine how many B2B collaboration users need paid Azure AD capabilities.</span><span class="sxs-lookup"><span data-stu-id="60087-133">The customer who owns the inviting tenant must be the one to determine how many B2B collaboration users need paid Azure AD capabilities.</span></span> <span data-ttu-id="60087-134">Depending on which paid Azure AD features you want for your guest users, you must have enough Azure AD paid licenses to cover B2B collaboration users in the 5:1 ratio.</span><span class="sxs-lookup"><span data-stu-id="60087-134">Depending on which paid Azure AD features you want for your guest users, you must have enough Azure AD paid licenses to cover B2B collaboration users in the 5:1 ratio.</span></span> 

## <a name="additional-licensing-details"></a><span data-ttu-id="60087-135">Additional licensing details</span><span class="sxs-lookup"><span data-stu-id="60087-135">Additional licensing details</span></span>
- <span data-ttu-id="60087-136">There is no need to actually assign licenses to B2B user accounts.</span><span class="sxs-lookup"><span data-stu-id="60087-136">There is no need to actually assign licenses to B2B user accounts.</span></span> <span data-ttu-id="60087-137">Based on the 5:1 ratio, licensing is automatically calculated and reported.</span><span class="sxs-lookup"><span data-stu-id="60087-137">Based on the 5:1 ratio, licensing is automatically calculated and reported.</span></span>
- <span data-ttu-id="60087-138">If no paid Azure AD license exists in the tenant, every invited user gets the rights that the Azure AD Free edition offers.</span><span class="sxs-lookup"><span data-stu-id="60087-138">If no paid Azure AD license exists in the tenant, every invited user gets the rights that the Azure AD Free edition offers.</span></span>
- <span data-ttu-id="60087-139">If a B2B collaboration user already has a paid Azure AD license from their organization, they do not consume one of the B2B collaboration licenses of the inviting tenant.</span><span class="sxs-lookup"><span data-stu-id="60087-139">If a B2B collaboration user already has a paid Azure AD license from their organization, they do not consume one of the B2B collaboration licenses of the inviting tenant.</span></span>

## <a name="advanced-discussion-what-are-the-licensing-considerations-when-we-add-users-from-a-conglomerate-organization-as-members-using-your-apis"></a><span data-ttu-id="60087-140">Advanced discussion: What are the licensing considerations when we add users from a conglomerate organization as “members” using your APIs?</span><span class="sxs-lookup"><span data-stu-id="60087-140">Advanced discussion: What are the licensing considerations when we add users from a conglomerate organization as “members” using your APIs?</span></span>
<span data-ttu-id="60087-141">A B2B guest user is one that is invited from a partner organization to work with the host organization.</span><span class="sxs-lookup"><span data-stu-id="60087-141">A B2B guest user is one that is invited from a partner organization to work with the host organization.</span></span> <span data-ttu-id="60087-142">Typically, any other case does not qualify as B2B even it uses B2B features.</span><span class="sxs-lookup"><span data-stu-id="60087-142">Typically, any other case does not qualify as B2B even it uses B2B features.</span></span> <span data-ttu-id="60087-143">Let’s look at two cases in particular:</span><span class="sxs-lookup"><span data-stu-id="60087-143">Let’s look at two cases in particular:</span></span>

1. <span data-ttu-id="60087-144">If a host invites an employee using a consumer address</span><span class="sxs-lookup"><span data-stu-id="60087-144">If a host invites an employee using a consumer address</span></span>
  * <span data-ttu-id="60087-145">This scenario is not compliant with our licensing policies and is not recommended.</span><span class="sxs-lookup"><span data-stu-id="60087-145">This scenario is not compliant with our licensing policies and is not recommended.</span></span>

2. <span data-ttu-id="60087-146">If a host organization adds a user from another conglomerate organization</span><span class="sxs-lookup"><span data-stu-id="60087-146">If a host organization adds a user from another conglomerate organization</span></span>
  1. <span data-ttu-id="60087-147">In this case, the user is invited using B2B APIs, but this case is not traditionally B2B.</span><span class="sxs-lookup"><span data-stu-id="60087-147">In this case, the user is invited using B2B APIs, but this case is not traditionally B2B.</span></span> <span data-ttu-id="60087-148">Ideally, we should have these organizations invite the other orgs users as members (our API allows that).</span><span class="sxs-lookup"><span data-stu-id="60087-148">Ideally, we should have these organizations invite the other orgs users as members (our API allows that).</span></span> <span data-ttu-id="60087-149">In this case, licenses have to be assigned to these members for them to access resources in the inviting organization.</span><span class="sxs-lookup"><span data-stu-id="60087-149">In this case, licenses have to be assigned to these members for them to access resources in the inviting organization.</span></span>

  2. <span data-ttu-id="60087-150">Some organizations may want to add the other org’s users to be added as “Guest” as a policy.</span><span class="sxs-lookup"><span data-stu-id="60087-150">Some organizations may want to add the other org’s users to be added as “Guest” as a policy.</span></span> <span data-ttu-id="60087-151">There are two cases here:</span><span class="sxs-lookup"><span data-stu-id="60087-151">There are two cases here:</span></span>
      * <span data-ttu-id="60087-152">The conglomerate organization is already using Azure AD and the invited users are licensed in the other organization: in this case, we don’t expect invited users to need to follow the 1:5 formula laid out earlier in this document.</span><span class="sxs-lookup"><span data-stu-id="60087-152">The conglomerate organization is already using Azure AD and the invited users are licensed in the other organization: in this case, we don’t expect invited users to need to follow the 1:5 formula laid out earlier in this document.</span></span> 

      * <span data-ttu-id="60087-153">The conglomerate organization is not using Azure AD or doesn’t have adequate licenses: In this case, follow the 1:5 formula laid out earlier in this document.</span><span class="sxs-lookup"><span data-stu-id="60087-153">The conglomerate organization is not using Azure AD or doesn’t have adequate licenses: In this case, follow the 1:5 formula laid out earlier in this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60087-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="60087-154">Next steps</span></span>

<span data-ttu-id="60087-155">See the following articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="60087-155">See the following articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="60087-156">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="60087-156">What is Azure AD B2B collaboration?</span></span>](what-is-b2b.md)
* [<span data-ttu-id="60087-157">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="60087-157">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](faq.md)