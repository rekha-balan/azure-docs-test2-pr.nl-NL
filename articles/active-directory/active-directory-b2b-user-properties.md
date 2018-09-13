---
title: Properties of an Azure Active Directory B2B collaboration user | Microsoft Docs
description: Azure Active Directory B2B collaboration user properties are configurable
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
ms.date: 04/12/2017
ms.author: sasubram
ms.openlocfilehash: 76359ba7a0346250e26b5f1e248d0b3c5f138869
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553856"
---
# <a name="properties-of-an-azure-active-directory-b2b-collaboration-user"></a><span data-ttu-id="3a4bd-103">Properties of an Azure Active Directory B2B collaboration user</span><span class="sxs-lookup"><span data-stu-id="3a4bd-103">Properties of an Azure Active Directory B2B collaboration user</span></span>

<span data-ttu-id="3a4bd-104">An Azure Active Directory (Azure AD) business-to-business (B2B) collaboration user is a user with UserType = Guest.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-104">An Azure Active Directory (Azure AD) business-to-business (B2B) collaboration user is a user with UserType = Guest.</span></span> <span data-ttu-id="3a4bd-105">This guest user typically is from a partner organization and has limited privileges in the inviting directory, by default.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-105">This guest user typically is from a partner organization and has limited privileges in the inviting directory, by default.</span></span>

<span data-ttu-id="3a4bd-106">Depending on the inviting organization's needs, an Azure AD B2B collaboration user can be in one of the following account states:</span><span class="sxs-lookup"><span data-stu-id="3a4bd-106">Depending on the inviting organization's needs, an Azure AD B2B collaboration user can be in one of the following account states:</span></span>

- <span data-ttu-id="3a4bd-107">State 1: Homed in an external instance of Azure AD and represented as a guest user in the host organization.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-107">State 1: Homed in an external instance of Azure AD and represented as a guest user in the host organization.</span></span> <span data-ttu-id="3a4bd-108">In this case, the B2B user signs in by using an Azure AD account that belongs to his home tenancy.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-108">In this case, the B2B user signs in by using an Azure AD account that belongs to his home tenancy.</span></span> <span data-ttu-id="3a4bd-109">If the external organization of the user doesn't use Azure AD at the time of invitation, the guest user in Azure AD is created when the user redeems his invitation and after Azure AD verifies his email address.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-109">If the external organization of the user doesn't use Azure AD at the time of invitation, the guest user in Azure AD is created when the user redeems his invitation and after Azure AD verifies his email address.</span></span> <span data-ttu-id="3a4bd-110">This is also called a just-in-time (JIT) tenancy or a viral tenancy.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-110">This is also called a just-in-time (JIT) tenancy or a viral tenancy.</span></span>

- <span data-ttu-id="3a4bd-111">State 2: Homed in a Microsoft account and represented as a guest user in the host organization.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-111">State 2: Homed in a Microsoft account and represented as a guest user in the host organization.</span></span> <span data-ttu-id="3a4bd-112">In this case, the guest user signs in with a Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-112">In this case, the guest user signs in with a Microsoft account.</span></span> <span data-ttu-id="3a4bd-113">The invited user's social identity (google.com or similar), which is not a Microsoft account, is created as a Microsoft account during offer redemption.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-113">The invited user's social identity (google.com or similar), which is not a Microsoft account, is created as a Microsoft account during offer redemption.</span></span>

- <span data-ttu-id="3a4bd-114">State 3: Homed in the host organization's on-premises Active Directory and synced with the host organization's Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-114">State 3: Homed in the host organization's on-premises Active Directory and synced with the host organization's Azure AD.</span></span> <span data-ttu-id="3a4bd-115">During this release, you must use PowerShell to manually change the UserType of such users in the cloud.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-115">During this release, you must use PowerShell to manually change the UserType of such users in the cloud.</span></span>

- <span data-ttu-id="3a4bd-116">State 4: Homed in host organization's Azure AD with UserType = Guest and credentials that the host organization manages.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-116">State 4: Homed in host organization's Azure AD with UserType = Guest and credentials that the host organization manages.</span></span>

  ![Displaying the inviter's initials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-user-properties/redemption-diagram.png)


<span data-ttu-id="3a4bd-118">Now, let's see what an Azure AD B2B collaboration user in State 1 looks like in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-118">Now, let's see what an Azure AD B2B collaboration user in State 1 looks like in Azure AD.</span></span>

### <a name="before-invitation-redemption"></a><span data-ttu-id="3a4bd-119">Before invitation redemption</span><span class="sxs-lookup"><span data-stu-id="3a4bd-119">Before invitation redemption</span></span>

![Before offer redemption](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-user-properties/before-redemption.png)

### <a name="after-invitation-redemption"></a><span data-ttu-id="3a4bd-121">After invitation redemption</span><span class="sxs-lookup"><span data-stu-id="3a4bd-121">After invitation redemption</span></span>

![After offer redemption](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-user-properties/after-redemption.png)

## <a name="key-properties-of-the-azure-ad-b2b-collaboration-user"></a><span data-ttu-id="3a4bd-123">Key properties of the Azure AD B2B collaboration user</span><span class="sxs-lookup"><span data-stu-id="3a4bd-123">Key properties of the Azure AD B2B collaboration user</span></span>
### <a name="usertype"></a><span data-ttu-id="3a4bd-124">UserType</span><span class="sxs-lookup"><span data-stu-id="3a4bd-124">UserType</span></span>
<span data-ttu-id="3a4bd-125">This property indicates the relationship of the user to the host tenancy.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-125">This property indicates the relationship of the user to the host tenancy.</span></span> <span data-ttu-id="3a4bd-126">This can have two values:</span><span class="sxs-lookup"><span data-stu-id="3a4bd-126">This can have two values:</span></span>
- <span data-ttu-id="3a4bd-127">Member: This value indicates an employee of the host organization and a user in the organization's payroll.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-127">Member: This value indicates an employee of the host organization and a user in the organization's payroll.</span></span> <span data-ttu-id="3a4bd-128">For example, this user expects to have access to internal-only sites.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-128">For example, this user expects to have access to internal-only sites.</span></span> <span data-ttu-id="3a4bd-129">This user would not be considered an external collaborator.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-129">This user would not be considered an external collaborator.</span></span>

- <span data-ttu-id="3a4bd-130">Guest: This value indicates a user who isn't considered internal to the company.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-130">Guest: This value indicates a user who isn't considered internal to the company.</span></span> <span data-ttu-id="3a4bd-131">This user could be an external collaborator, partner, customer, or similar user who isn't expected to get a CEO's internal memo, for example, or get company benefits.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-131">This user could be an external collaborator, partner, customer, or similar user who isn't expected to get a CEO's internal memo, for example, or get company benefits.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3a4bd-132">The UserType has no relation to how the user signs in, the directory role of the user, and so on.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-132">The UserType has no relation to how the user signs in, the directory role of the user, and so on.</span></span> <span data-ttu-id="3a4bd-133">This property simply indicates the user's relationship to the host organization and allows the organization to enforce policies that depend on this property.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-133">This property simply indicates the user's relationship to the host organization and allows the organization to enforce policies that depend on this property.</span></span>

### <a name="source"></a><span data-ttu-id="3a4bd-134">Source</span><span class="sxs-lookup"><span data-stu-id="3a4bd-134">Source</span></span>
<span data-ttu-id="3a4bd-135">This property indicates how the user signs in.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-135">This property indicates how the user signs in.</span></span>

- <span data-ttu-id="3a4bd-136">Invited User: This user has been invited but has not yet redeemed an invitation.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-136">Invited User: This user has been invited but has not yet redeemed an invitation.</span></span>

- <span data-ttu-id="3a4bd-137">External Active Directory: This user is homed in an external organization and authenticates by using an Azure AD account that belongs to the other organization.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-137">External Active Directory: This user is homed in an external organization and authenticates by using an Azure AD account that belongs to the other organization.</span></span> <span data-ttu-id="3a4bd-138">This type of sign-in corresponds to State 1.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-138">This type of sign-in corresponds to State 1.</span></span>

- <span data-ttu-id="3a4bd-139">Microsoft account: This user is homed in a Microsoft account and authenticates by using a Microsoft account.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-139">Microsoft account: This user is homed in a Microsoft account and authenticates by using a Microsoft account.</span></span> <span data-ttu-id="3a4bd-140">This type of sign-in corresponds to State 2.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-140">This type of sign-in corresponds to State 2.</span></span>

- <span data-ttu-id="3a4bd-141">Windows Server Active Directory: This user is signed in from on-premises Active Directory that belongs to this organization.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-141">Windows Server Active Directory: This user is signed in from on-premises Active Directory that belongs to this organization.</span></span> <span data-ttu-id="3a4bd-142">This type of sign-in corresponds to State 3.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-142">This type of sign-in corresponds to State 3.</span></span>

- <span data-ttu-id="3a4bd-143">Azure Active Directory: This user authenticates by using an Azure AD account that belongs to this organization.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-143">Azure Active Directory: This user authenticates by using an Azure AD account that belongs to this organization.</span></span> <span data-ttu-id="3a4bd-144">This type of sign-in corresponds to State 4.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-144">This type of sign-in corresponds to State 4.</span></span>
  > [!NOTE]
  > <span data-ttu-id="3a4bd-145">Source and UserType are independent properties.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-145">Source and UserType are independent properties.</span></span> <span data-ttu-id="3a4bd-146">A value of Source does not imply a particular value for UserType.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-146">A value of Source does not imply a particular value for UserType.</span></span>

## <a name="can-azure-ad-b2b-users-be-added-as-members-instead-of-guests"></a><span data-ttu-id="3a4bd-147">Can Azure AD B2B users be added as members instead of guests?</span><span class="sxs-lookup"><span data-stu-id="3a4bd-147">Can Azure AD B2B users be added as members instead of guests?</span></span>
<span data-ttu-id="3a4bd-148">Typically, an Azure AD B2B user and guest user are synonymous.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-148">Typically, an Azure AD B2B user and guest user are synonymous.</span></span> <span data-ttu-id="3a4bd-149">Therefore, an Azure AD B2B collaboration user is added as a user with UserType = Guest by default.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-149">Therefore, an Azure AD B2B collaboration user is added as a user with UserType = Guest by default.</span></span> <span data-ttu-id="3a4bd-150">However, in some cases, the partner organization is a member of a larger organization to which the host organization also belongs.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-150">However, in some cases, the partner organization is a member of a larger organization to which the host organization also belongs.</span></span> <span data-ttu-id="3a4bd-151">If so, the host organization might want to treat users in the partner organization as members instead of guests.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-151">If so, the host organization might want to treat users in the partner organization as members instead of guests.</span></span> <span data-ttu-id="3a4bd-152">In this case, use the Azure AD B2B Invitation Manager APIs to add or invite a user from the partner organization to the host organization as a member.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-152">In this case, use the Azure AD B2B Invitation Manager APIs to add or invite a user from the partner organization to the host organization as a member.</span></span>

## <a name="filter-for-guest-users-in-the-directory"></a><span data-ttu-id="3a4bd-153">Filter for guest users in the directory</span><span class="sxs-lookup"><span data-stu-id="3a4bd-153">Filter for guest users in the directory</span></span>

![Filter guest users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-user-properties/filter-guest-users.png)

## <a name="convert-usertype"></a><span data-ttu-id="3a4bd-155">Convert UserType</span><span class="sxs-lookup"><span data-stu-id="3a4bd-155">Convert UserType</span></span>
<span data-ttu-id="3a4bd-156">Currently, it is possible for users to convert UserType from Member to Guest and vice-versa by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-156">Currently, it is possible for users to convert UserType from Member to Guest and vice-versa by using PowerShell.</span></span> <span data-ttu-id="3a4bd-157">However, the UserType property is supposed to represent the user's relationship to the organization.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-157">However, the UserType property is supposed to represent the user's relationship to the organization.</span></span> <span data-ttu-id="3a4bd-158">Therefore, the value of this property should change only if the relationship of the user to the organization changes.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-158">Therefore, the value of this property should change only if the relationship of the user to the organization changes.</span></span> <span data-ttu-id="3a4bd-159">If the relationship of the user changes, should issues, like whether the user principal name (UPN) should change, be addressed?</span><span class="sxs-lookup"><span data-stu-id="3a4bd-159">If the relationship of the user changes, should issues, like whether the user principal name (UPN) should change, be addressed?</span></span> <span data-ttu-id="3a4bd-160">Should the user continue to have access to the same resources?</span><span class="sxs-lookup"><span data-stu-id="3a4bd-160">Should the user continue to have access to the same resources?</span></span> <span data-ttu-id="3a4bd-161">Should a mailbox be assigned?</span><span class="sxs-lookup"><span data-stu-id="3a4bd-161">Should a mailbox be assigned?</span></span> <span data-ttu-id="3a4bd-162">Therefore, we do not recommend changing the UserType by using PowerShell as an atomic activity.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-162">Therefore, we do not recommend changing the UserType by using PowerShell as an atomic activity.</span></span> <span data-ttu-id="3a4bd-163">In addition, in case this property becomes immutable by using PowerShell, we do not recommend taking a dependency on this value.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-163">In addition, in case this property becomes immutable by using PowerShell, we do not recommend taking a dependency on this value.</span></span>

## <a name="remove-guest-user-limitations"></a><span data-ttu-id="3a4bd-164">Remove guest user limitations</span><span class="sxs-lookup"><span data-stu-id="3a4bd-164">Remove guest user limitations</span></span>
<span data-ttu-id="3a4bd-165">There may be cases where you want to give your guest users higher privileges.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-165">There may be cases where you want to give your guest users higher privileges.</span></span> <span data-ttu-id="3a4bd-166">In this situation, you can add a guest user to any role and even remove the default guest user restrictions in the directory to give a user the same privileges as members.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-166">In this situation, you can add a guest user to any role and even remove the default guest user restrictions in the directory to give a user the same privileges as members.</span></span>

<span data-ttu-id="3a4bd-167">It is possible to turn off the default guest user limitations so that a guest user in the company directory is given the same directory permissions as a regular user, who is a member.</span><span class="sxs-lookup"><span data-stu-id="3a4bd-167">It is possible to turn off the default guest user limitations so that a guest user in the company directory is given the same directory permissions as a regular user, who is a member.</span></span>

![Remove guest user limitations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-b2b-user-properties/remove-guest-limitations.png)

## <a name="next-steps"></a><span data-ttu-id="3a4bd-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="3a4bd-169">Next steps</span></span>

<span data-ttu-id="3a4bd-170">Browse our other articles on Azure AD B2B collaboration:</span><span class="sxs-lookup"><span data-stu-id="3a4bd-170">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="3a4bd-171">What is Azure AD B2B collaboration?</span><span class="sxs-lookup"><span data-stu-id="3a4bd-171">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="3a4bd-172">Adding a B2B collaboration user to a role</span><span class="sxs-lookup"><span data-stu-id="3a4bd-172">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="3a4bd-173">Delegate B2B collaboration invitations</span><span class="sxs-lookup"><span data-stu-id="3a4bd-173">Delegate B2B collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="3a4bd-174">B2B collaboration user auditing and reporting</span><span class="sxs-lookup"><span data-stu-id="3a4bd-174">B2B collaboration user auditing and reporting</span></span>](active-directory-b2b-auditing-and-reporting.md)
* [<span data-ttu-id="3a4bd-175">Dynamic groups and B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="3a4bd-175">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="3a4bd-176">B2B collaboration code and PowerShell samples</span><span class="sxs-lookup"><span data-stu-id="3a4bd-176">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="3a4bd-177">Configure SaaS apps for B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="3a4bd-177">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="3a4bd-178">B2B collaboration user tokens</span><span class="sxs-lookup"><span data-stu-id="3a4bd-178">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="3a4bd-179">B2B collaboration user claims mapping</span><span class="sxs-lookup"><span data-stu-id="3a4bd-179">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="3a4bd-180">Office 365 external sharing</span><span class="sxs-lookup"><span data-stu-id="3a4bd-180">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="3a4bd-181">B2B collaboration current limitations</span><span class="sxs-lookup"><span data-stu-id="3a4bd-181">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)





