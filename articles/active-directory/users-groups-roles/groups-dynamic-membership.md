---
title: Dynamic automatic group membership rules reference in Azure Active Directory | Microsoft Docs
description: How to create membership rules to automatically populate groups, and a rule reference.
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 08/01/2018
ms.author: curtand
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 9c0bb676cc59820d3ae83612893c8920d5d0aebe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866303"
---
# <a name="dynamic-membership-rules-for-groups-in-azure-active-directory"></a><span data-ttu-id="67954-103">Dynamic membership rules for groups in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67954-103">Dynamic membership rules for groups in Azure Active Directory</span></span>

<span data-ttu-id="67954-104">In Azure Active Directory (Azure AD), you can create complex attribute-based rules to enable dynamic memberships for groups.</span><span class="sxs-lookup"><span data-stu-id="67954-104">In Azure Active Directory (Azure AD), you can create complex attribute-based rules to enable dynamic memberships for groups.</span></span> <span data-ttu-id="67954-105">Dynamic group membership reduces the administrative overhead of adding and removing users.</span><span class="sxs-lookup"><span data-stu-id="67954-105">Dynamic group membership reduces the administrative overhead of adding and removing users.</span></span> <span data-ttu-id="67954-106">This article details the properties and syntax to create dynamic membership rules for users or devices.</span><span class="sxs-lookup"><span data-stu-id="67954-106">This article details the properties and syntax to create dynamic membership rules for users or devices.</span></span> <span data-ttu-id="67954-107">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span><span class="sxs-lookup"><span data-stu-id="67954-107">You can set up a rule for dynamic membership on security groups or Office 365 groups.</span></span>

<span data-ttu-id="67954-108">When any attributes of a user or device change, the system evaluates all dynamic group rules in a directory to see if the change would trigger any group adds or removes.</span><span class="sxs-lookup"><span data-stu-id="67954-108">When any attributes of a user or device change, the system evaluates all dynamic group rules in a directory to see if the change would trigger any group adds or removes.</span></span> <span data-ttu-id="67954-109">If a user or device satisfies a rule on a group, they are added as a member of that group.</span><span class="sxs-lookup"><span data-stu-id="67954-109">If a user or device satisfies a rule on a group, they are added as a member of that group.</span></span> <span data-ttu-id="67954-110">If they no longer satisfy the rule, they are removed.</span><span class="sxs-lookup"><span data-stu-id="67954-110">If they no longer satisfy the rule, they are removed.</span></span>

* <span data-ttu-id="67954-111">You can create a dynamic group for devices or for users, but you can't create a rule that contains both users and devices.</span><span class="sxs-lookup"><span data-stu-id="67954-111">You can create a dynamic group for devices or for users, but you can't create a rule that contains both users and devices.</span></span>
* <span data-ttu-id="67954-112">You can't create a device group based on the device owners' attributes.</span><span class="sxs-lookup"><span data-stu-id="67954-112">You can't create a device group based on the device owners' attributes.</span></span> <span data-ttu-id="67954-113">Device membership rules can only reference device attributes.</span><span class="sxs-lookup"><span data-stu-id="67954-113">Device membership rules can only reference device attributes.</span></span>

> [!NOTE]
> <span data-ttu-id="67954-114">This feature requires an Azure AD Premium P1 license for each unique user that is a member of one or more dynamic groups.</span><span class="sxs-lookup"><span data-stu-id="67954-114">This feature requires an Azure AD Premium P1 license for each unique user that is a member of one or more dynamic groups.</span></span> <span data-ttu-id="67954-115">You don't have to assign licenses to users for them to be members of dynamic groups, but you must have the minimum number of licenses in the tenant to cover all such users.</span><span class="sxs-lookup"><span data-stu-id="67954-115">You don't have to assign licenses to users for them to be members of dynamic groups, but you must have the minimum number of licenses in the tenant to cover all such users.</span></span> <span data-ttu-id="67954-116">For example, if you had a total of 1,000 unique users in all dynamic groups in your tenant, you would need at least 1,000 licenses for Azure AD Premium P1 to meet the license requirement.</span><span class="sxs-lookup"><span data-stu-id="67954-116">For example, if you had a total of 1,000 unique users in all dynamic groups in your tenant, you would need at least 1,000 licenses for Azure AD Premium P1 to meet the license requirement.</span></span>
>

## <a name="constructing-the-body-of-a-membership-rule"></a><span data-ttu-id="67954-117">Constructing the body of a membership rule</span><span class="sxs-lookup"><span data-stu-id="67954-117">Constructing the body of a membership rule</span></span>

<span data-ttu-id="67954-118">A membership rule that automatically populates a group with users or devices is a binary expression that results in a true or false outcome.</span><span class="sxs-lookup"><span data-stu-id="67954-118">A membership rule that automatically populates a group with users or devices is a binary expression that results in a true or false outcome.</span></span> <span data-ttu-id="67954-119">The three parts of a simple rule are:</span><span class="sxs-lookup"><span data-stu-id="67954-119">The three parts of a simple rule are:</span></span>

* <span data-ttu-id="67954-120">Property</span><span class="sxs-lookup"><span data-stu-id="67954-120">Property</span></span>
* <span data-ttu-id="67954-121">Operator</span><span class="sxs-lookup"><span data-stu-id="67954-121">Operator</span></span>
* <span data-ttu-id="67954-122">Value</span><span class="sxs-lookup"><span data-stu-id="67954-122">Value</span></span>

<span data-ttu-id="67954-123">The order of the parts within an expression are important to avoid syntax errors.</span><span class="sxs-lookup"><span data-stu-id="67954-123">The order of the parts within an expression are important to avoid syntax errors.</span></span>

### <a name="rules-with-a-single-expression"></a><span data-ttu-id="67954-124">Rules with a single expression</span><span class="sxs-lookup"><span data-stu-id="67954-124">Rules with a single expression</span></span>

<span data-ttu-id="67954-125">A single expression is the simplest form of a membership rule and only has the three parts mentioned above.</span><span class="sxs-lookup"><span data-stu-id="67954-125">A single expression is the simplest form of a membership rule and only has the three parts mentioned above.</span></span> <span data-ttu-id="67954-126">A rule with a single expression looks similar to this: `Property Operator Value`, where the syntax for the property is the name of object.property.</span><span class="sxs-lookup"><span data-stu-id="67954-126">A rule with a single expression looks similar to this: `Property Operator Value`, where the syntax for the property is the name of object.property.</span></span>

<span data-ttu-id="67954-127">The following is an example of a properly constructed membership rule with a single expression:</span><span class="sxs-lookup"><span data-stu-id="67954-127">The following is an example of a properly constructed membership rule with a single expression:</span></span>

```
user.department -eq "Sales"
```

<span data-ttu-id="67954-128">Parentheses are optional for a single expression.</span><span class="sxs-lookup"><span data-stu-id="67954-128">Parentheses are optional for a single expression.</span></span> <span data-ttu-id="67954-129">The total length of the body of your membership rule cannot exceed 2048 characters.</span><span class="sxs-lookup"><span data-stu-id="67954-129">The total length of the body of your membership rule cannot exceed 2048 characters.</span></span>

## <a name="supported-properties"></a><span data-ttu-id="67954-130">Supported properties</span><span class="sxs-lookup"><span data-stu-id="67954-130">Supported properties</span></span>

<span data-ttu-id="67954-131">There are three types of properties that can be used to construct a membership rule.</span><span class="sxs-lookup"><span data-stu-id="67954-131">There are three types of properties that can be used to construct a membership rule.</span></span>

* <span data-ttu-id="67954-132">Boolean</span><span class="sxs-lookup"><span data-stu-id="67954-132">Boolean</span></span>
* <span data-ttu-id="67954-133">String</span><span class="sxs-lookup"><span data-stu-id="67954-133">String</span></span>
* <span data-ttu-id="67954-134">String collection</span><span class="sxs-lookup"><span data-stu-id="67954-134">String collection</span></span>

<span data-ttu-id="67954-135">The following are the user properties that you can use to create a single expression.</span><span class="sxs-lookup"><span data-stu-id="67954-135">The following are the user properties that you can use to create a single expression.</span></span>

### <a name="properties-of-type-boolean"></a><span data-ttu-id="67954-136">Properties of type boolean</span><span class="sxs-lookup"><span data-stu-id="67954-136">Properties of type boolean</span></span>

| <span data-ttu-id="67954-137">Properties</span><span class="sxs-lookup"><span data-stu-id="67954-137">Properties</span></span> | <span data-ttu-id="67954-138">Allowed values</span><span class="sxs-lookup"><span data-stu-id="67954-138">Allowed values</span></span> | <span data-ttu-id="67954-139">Usage</span><span class="sxs-lookup"><span data-stu-id="67954-139">Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67954-140">accountEnabled</span><span class="sxs-lookup"><span data-stu-id="67954-140">accountEnabled</span></span> |<span data-ttu-id="67954-141">true false</span><span class="sxs-lookup"><span data-stu-id="67954-141">true false</span></span> |<span data-ttu-id="67954-142">user.accountEnabled -eq true</span><span class="sxs-lookup"><span data-stu-id="67954-142">user.accountEnabled -eq true</span></span> |
| <span data-ttu-id="67954-143">dirSyncEnabled</span><span class="sxs-lookup"><span data-stu-id="67954-143">dirSyncEnabled</span></span> |<span data-ttu-id="67954-144">true false</span><span class="sxs-lookup"><span data-stu-id="67954-144">true false</span></span> |<span data-ttu-id="67954-145">user.dirSyncEnabled -eq true</span><span class="sxs-lookup"><span data-stu-id="67954-145">user.dirSyncEnabled -eq true</span></span> |

### <a name="properties-of-type-string"></a><span data-ttu-id="67954-146">Properties of type string</span><span class="sxs-lookup"><span data-stu-id="67954-146">Properties of type string</span></span>

| <span data-ttu-id="67954-147">Properties</span><span class="sxs-lookup"><span data-stu-id="67954-147">Properties</span></span> | <span data-ttu-id="67954-148">Allowed values</span><span class="sxs-lookup"><span data-stu-id="67954-148">Allowed values</span></span> | <span data-ttu-id="67954-149">Usage</span><span class="sxs-lookup"><span data-stu-id="67954-149">Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67954-150">city</span><span class="sxs-lookup"><span data-stu-id="67954-150">city</span></span> |<span data-ttu-id="67954-151">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-151">Any string value or *null*</span></span> |<span data-ttu-id="67954-152">(user.city -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-152">(user.city -eq "value")</span></span> |
| <span data-ttu-id="67954-153">country</span><span class="sxs-lookup"><span data-stu-id="67954-153">country</span></span> |<span data-ttu-id="67954-154">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-154">Any string value or *null*</span></span> |<span data-ttu-id="67954-155">(user.country -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-155">(user.country -eq "value")</span></span> |
| <span data-ttu-id="67954-156">companyName</span><span class="sxs-lookup"><span data-stu-id="67954-156">companyName</span></span> | <span data-ttu-id="67954-157">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-157">Any string value or *null*</span></span> | <span data-ttu-id="67954-158">(user.companyName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-158">(user.companyName -eq "value")</span></span> |
| <span data-ttu-id="67954-159">department</span><span class="sxs-lookup"><span data-stu-id="67954-159">department</span></span> |<span data-ttu-id="67954-160">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-160">Any string value or *null*</span></span> |<span data-ttu-id="67954-161">(user.department -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-161">(user.department -eq "value")</span></span> |
| <span data-ttu-id="67954-162">displayName</span><span class="sxs-lookup"><span data-stu-id="67954-162">displayName</span></span> |<span data-ttu-id="67954-163">Any string value</span><span class="sxs-lookup"><span data-stu-id="67954-163">Any string value</span></span> |<span data-ttu-id="67954-164">(user.displayName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-164">(user.displayName -eq "value")</span></span> |
| <span data-ttu-id="67954-165">employeeId</span><span class="sxs-lookup"><span data-stu-id="67954-165">employeeId</span></span> |<span data-ttu-id="67954-166">Any string value</span><span class="sxs-lookup"><span data-stu-id="67954-166">Any string value</span></span> |<span data-ttu-id="67954-167">(user.employeeId -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-167">(user.employeeId -eq "value")</span></span><br><span data-ttu-id="67954-168">(user.employeeId -ne *null*)</span><span class="sxs-lookup"><span data-stu-id="67954-168">(user.employeeId -ne *null*)</span></span> |
| <span data-ttu-id="67954-169">facsimileTelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="67954-169">facsimileTelephoneNumber</span></span> |<span data-ttu-id="67954-170">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-170">Any string value or *null*</span></span> |<span data-ttu-id="67954-171">(user.facsimileTelephoneNumber -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-171">(user.facsimileTelephoneNumber -eq "value")</span></span> |
| <span data-ttu-id="67954-172">givenName</span><span class="sxs-lookup"><span data-stu-id="67954-172">givenName</span></span> |<span data-ttu-id="67954-173">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-173">Any string value or *null*</span></span> |<span data-ttu-id="67954-174">(user.givenName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-174">(user.givenName -eq "value")</span></span> |
| <span data-ttu-id="67954-175">jobTitle</span><span class="sxs-lookup"><span data-stu-id="67954-175">jobTitle</span></span> |<span data-ttu-id="67954-176">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-176">Any string value or *null*</span></span> |<span data-ttu-id="67954-177">(user.jobTitle -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-177">(user.jobTitle -eq "value")</span></span> |
| <span data-ttu-id="67954-178">mail</span><span class="sxs-lookup"><span data-stu-id="67954-178">mail</span></span> |<span data-ttu-id="67954-179">Any string value or *null* (SMTP address of the user)</span><span class="sxs-lookup"><span data-stu-id="67954-179">Any string value or *null* (SMTP address of the user)</span></span> |<span data-ttu-id="67954-180">(user.mail -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-180">(user.mail -eq "value")</span></span> |
| <span data-ttu-id="67954-181">mailNickName</span><span class="sxs-lookup"><span data-stu-id="67954-181">mailNickName</span></span> |<span data-ttu-id="67954-182">Any string value (mail alias of the user)</span><span class="sxs-lookup"><span data-stu-id="67954-182">Any string value (mail alias of the user)</span></span> |<span data-ttu-id="67954-183">(user.mailNickName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-183">(user.mailNickName -eq "value")</span></span> |
| <span data-ttu-id="67954-184">mobile</span><span class="sxs-lookup"><span data-stu-id="67954-184">mobile</span></span> |<span data-ttu-id="67954-185">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-185">Any string value or *null*</span></span> |<span data-ttu-id="67954-186">(user.mobile -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-186">(user.mobile -eq "value")</span></span> |
| <span data-ttu-id="67954-187">objectId</span><span class="sxs-lookup"><span data-stu-id="67954-187">objectId</span></span> |<span data-ttu-id="67954-188">GUID of the user object</span><span class="sxs-lookup"><span data-stu-id="67954-188">GUID of the user object</span></span> |<span data-ttu-id="67954-189">(user.objectId -eq "11111111-1111-1111-1111-111111111111")</span><span class="sxs-lookup"><span data-stu-id="67954-189">(user.objectId -eq "11111111-1111-1111-1111-111111111111")</span></span> |
| <span data-ttu-id="67954-190">onPremisesSecurityIdentifier</span><span class="sxs-lookup"><span data-stu-id="67954-190">onPremisesSecurityIdentifier</span></span> | <span data-ttu-id="67954-191">On-premises security identifier (SID) for users who were synchronized from on-premises to the cloud.</span><span class="sxs-lookup"><span data-stu-id="67954-191">On-premises security identifier (SID) for users who were synchronized from on-premises to the cloud.</span></span> |<span data-ttu-id="67954-192">(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111")</span><span class="sxs-lookup"><span data-stu-id="67954-192">(user.onPremisesSecurityIdentifier -eq "S-1-1-11-1111111111-1111111111-1111111111-1111111")</span></span> |
| <span data-ttu-id="67954-193">passwordPolicies</span><span class="sxs-lookup"><span data-stu-id="67954-193">passwordPolicies</span></span> |<span data-ttu-id="67954-194">None DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword</span><span class="sxs-lookup"><span data-stu-id="67954-194">None DisableStrongPassword DisablePasswordExpiration DisablePasswordExpiration, DisableStrongPassword</span></span> |<span data-ttu-id="67954-195">(user.passwordPolicies -eq "DisableStrongPassword")</span><span class="sxs-lookup"><span data-stu-id="67954-195">(user.passwordPolicies -eq "DisableStrongPassword")</span></span> |
| <span data-ttu-id="67954-196">physicalDeliveryOfficeName</span><span class="sxs-lookup"><span data-stu-id="67954-196">physicalDeliveryOfficeName</span></span> |<span data-ttu-id="67954-197">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-197">Any string value or *null*</span></span> |<span data-ttu-id="67954-198">(user.physicalDeliveryOfficeName -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-198">(user.physicalDeliveryOfficeName -eq "value")</span></span> |
| <span data-ttu-id="67954-199">postalCode</span><span class="sxs-lookup"><span data-stu-id="67954-199">postalCode</span></span> |<span data-ttu-id="67954-200">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-200">Any string value or *null*</span></span> |<span data-ttu-id="67954-201">(user.postalCode -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-201">(user.postalCode -eq "value")</span></span> |
| <span data-ttu-id="67954-202">preferredLanguage</span><span class="sxs-lookup"><span data-stu-id="67954-202">preferredLanguage</span></span> |<span data-ttu-id="67954-203">ISO 639-1 code</span><span class="sxs-lookup"><span data-stu-id="67954-203">ISO 639-1 code</span></span> |<span data-ttu-id="67954-204">(user.preferredLanguage -eq "en-US")</span><span class="sxs-lookup"><span data-stu-id="67954-204">(user.preferredLanguage -eq "en-US")</span></span> |
| <span data-ttu-id="67954-205">sipProxyAddress</span><span class="sxs-lookup"><span data-stu-id="67954-205">sipProxyAddress</span></span> |<span data-ttu-id="67954-206">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-206">Any string value or *null*</span></span> |<span data-ttu-id="67954-207">(user.sipProxyAddress -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-207">(user.sipProxyAddress -eq "value")</span></span> |
| <span data-ttu-id="67954-208">state</span><span class="sxs-lookup"><span data-stu-id="67954-208">state</span></span> |<span data-ttu-id="67954-209">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-209">Any string value or *null*</span></span> |<span data-ttu-id="67954-210">(user.state -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-210">(user.state -eq "value")</span></span> |
| <span data-ttu-id="67954-211">streetAddress</span><span class="sxs-lookup"><span data-stu-id="67954-211">streetAddress</span></span> |<span data-ttu-id="67954-212">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-212">Any string value or *null*</span></span> |<span data-ttu-id="67954-213">(user.streetAddress -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-213">(user.streetAddress -eq "value")</span></span> |
| <span data-ttu-id="67954-214">surname</span><span class="sxs-lookup"><span data-stu-id="67954-214">surname</span></span> |<span data-ttu-id="67954-215">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-215">Any string value or *null*</span></span> |<span data-ttu-id="67954-216">(user.surname -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-216">(user.surname -eq "value")</span></span> |
| <span data-ttu-id="67954-217">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="67954-217">telephoneNumber</span></span> |<span data-ttu-id="67954-218">Any string value or *null*</span><span class="sxs-lookup"><span data-stu-id="67954-218">Any string value or *null*</span></span> |<span data-ttu-id="67954-219">(user.telephoneNumber -eq "value")</span><span class="sxs-lookup"><span data-stu-id="67954-219">(user.telephoneNumber -eq "value")</span></span> |
| <span data-ttu-id="67954-220">usageLocation</span><span class="sxs-lookup"><span data-stu-id="67954-220">usageLocation</span></span> |<span data-ttu-id="67954-221">Two lettered country code</span><span class="sxs-lookup"><span data-stu-id="67954-221">Two lettered country code</span></span> |<span data-ttu-id="67954-222">(user.usageLocation -eq "US")</span><span class="sxs-lookup"><span data-stu-id="67954-222">(user.usageLocation -eq "US")</span></span> |
| <span data-ttu-id="67954-223">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="67954-223">userPrincipalName</span></span> |<span data-ttu-id="67954-224">Any string value</span><span class="sxs-lookup"><span data-stu-id="67954-224">Any string value</span></span> |<span data-ttu-id="67954-225">(user.userPrincipalName -eq "alias@domain")</span><span class="sxs-lookup"><span data-stu-id="67954-225">(user.userPrincipalName -eq "alias@domain")</span></span> |
| <span data-ttu-id="67954-226">userType</span><span class="sxs-lookup"><span data-stu-id="67954-226">userType</span></span> |<span data-ttu-id="67954-227">member guest *null*</span><span class="sxs-lookup"><span data-stu-id="67954-227">member guest *null*</span></span> |<span data-ttu-id="67954-228">(user.userType -eq "Member")</span><span class="sxs-lookup"><span data-stu-id="67954-228">(user.userType -eq "Member")</span></span> |

### <a name="properties-of-type-string-collection"></a><span data-ttu-id="67954-229">Properties of type string collection</span><span class="sxs-lookup"><span data-stu-id="67954-229">Properties of type string collection</span></span>

| <span data-ttu-id="67954-230">Properties</span><span class="sxs-lookup"><span data-stu-id="67954-230">Properties</span></span> | <span data-ttu-id="67954-231">Allowed values</span><span class="sxs-lookup"><span data-stu-id="67954-231">Allowed values</span></span> | <span data-ttu-id="67954-232">Usage</span><span class="sxs-lookup"><span data-stu-id="67954-232">Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67954-233">otherMails</span><span class="sxs-lookup"><span data-stu-id="67954-233">otherMails</span></span> |<span data-ttu-id="67954-234">Any string value</span><span class="sxs-lookup"><span data-stu-id="67954-234">Any string value</span></span> |<span data-ttu-id="67954-235">(user.otherMails -contains "alias@domain")</span><span class="sxs-lookup"><span data-stu-id="67954-235">(user.otherMails -contains "alias@domain")</span></span> |
| <span data-ttu-id="67954-236">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="67954-236">proxyAddresses</span></span> |<span data-ttu-id="67954-237">SMTP: alias@domain smtp: alias@domain</span><span class="sxs-lookup"><span data-stu-id="67954-237">SMTP: alias@domain smtp: alias@domain</span></span> |<span data-ttu-id="67954-238">(user.proxyAddresses -contains "SMTP: alias@domain")</span><span class="sxs-lookup"><span data-stu-id="67954-238">(user.proxyAddresses -contains "SMTP: alias@domain")</span></span> |

<span data-ttu-id="67954-239">For the properties used for device rules, see [Rules for devices](#rules-for-devices).</span><span class="sxs-lookup"><span data-stu-id="67954-239">For the properties used for device rules, see [Rules for devices](#rules-for-devices).</span></span>

## <a name="supported-operators"></a><span data-ttu-id="67954-240">Supported operators</span><span class="sxs-lookup"><span data-stu-id="67954-240">Supported operators</span></span>

<span data-ttu-id="67954-241">The following table lists all the supported operators and their syntax for a single expression.</span><span class="sxs-lookup"><span data-stu-id="67954-241">The following table lists all the supported operators and their syntax for a single expression.</span></span> <span data-ttu-id="67954-242">Operators can be used with or without the hyphen (-) prefix.</span><span class="sxs-lookup"><span data-stu-id="67954-242">Operators can be used with or without the hyphen (-) prefix.</span></span>

| <span data-ttu-id="67954-243">Operator</span><span class="sxs-lookup"><span data-stu-id="67954-243">Operator</span></span> | <span data-ttu-id="67954-244">Syntax</span><span class="sxs-lookup"><span data-stu-id="67954-244">Syntax</span></span> |
| --- | --- |
| <span data-ttu-id="67954-245">Not Equals</span><span class="sxs-lookup"><span data-stu-id="67954-245">Not Equals</span></span> |<span data-ttu-id="67954-246">-ne</span><span class="sxs-lookup"><span data-stu-id="67954-246">-ne</span></span> |
| <span data-ttu-id="67954-247">Equals</span><span class="sxs-lookup"><span data-stu-id="67954-247">Equals</span></span> |<span data-ttu-id="67954-248">-eq</span><span class="sxs-lookup"><span data-stu-id="67954-248">-eq</span></span> |
| <span data-ttu-id="67954-249">Not Starts With</span><span class="sxs-lookup"><span data-stu-id="67954-249">Not Starts With</span></span> |<span data-ttu-id="67954-250">-notStartsWith</span><span class="sxs-lookup"><span data-stu-id="67954-250">-notStartsWith</span></span> |
| <span data-ttu-id="67954-251">Starts With</span><span class="sxs-lookup"><span data-stu-id="67954-251">Starts With</span></span> |<span data-ttu-id="67954-252">-startsWith</span><span class="sxs-lookup"><span data-stu-id="67954-252">-startsWith</span></span> |
| <span data-ttu-id="67954-253">Not Contains</span><span class="sxs-lookup"><span data-stu-id="67954-253">Not Contains</span></span> |<span data-ttu-id="67954-254">-notContains</span><span class="sxs-lookup"><span data-stu-id="67954-254">-notContains</span></span> |
| <span data-ttu-id="67954-255">Contains</span><span class="sxs-lookup"><span data-stu-id="67954-255">Contains</span></span> |<span data-ttu-id="67954-256">-contains</span><span class="sxs-lookup"><span data-stu-id="67954-256">-contains</span></span> |
| <span data-ttu-id="67954-257">Not Match</span><span class="sxs-lookup"><span data-stu-id="67954-257">Not Match</span></span> |<span data-ttu-id="67954-258">-notMatch</span><span class="sxs-lookup"><span data-stu-id="67954-258">-notMatch</span></span> |
| <span data-ttu-id="67954-259">Match</span><span class="sxs-lookup"><span data-stu-id="67954-259">Match</span></span> |<span data-ttu-id="67954-260">-match</span><span class="sxs-lookup"><span data-stu-id="67954-260">-match</span></span> |
| <span data-ttu-id="67954-261">In</span><span class="sxs-lookup"><span data-stu-id="67954-261">In</span></span> | <span data-ttu-id="67954-262">-in</span><span class="sxs-lookup"><span data-stu-id="67954-262">-in</span></span> |
| <span data-ttu-id="67954-263">Not In</span><span class="sxs-lookup"><span data-stu-id="67954-263">Not In</span></span> | <span data-ttu-id="67954-264">-notIn</span><span class="sxs-lookup"><span data-stu-id="67954-264">-notIn</span></span> |

### <a name="using-the--in-and--notin-operators"></a><span data-ttu-id="67954-265">Using the -In and -notIn operators</span><span class="sxs-lookup"><span data-stu-id="67954-265">Using the -In and -notIn operators</span></span>

<span data-ttu-id="67954-266">If you want to compare the value of a user attribute against a number of different values you can use the -In or -notIn operators.</span><span class="sxs-lookup"><span data-stu-id="67954-266">If you want to compare the value of a user attribute against a number of different values you can use the -In or -notIn operators.</span></span> <span data-ttu-id="67954-267">Use the bracket symbols "[" and "]" to begin and end the list of values.</span><span class="sxs-lookup"><span data-stu-id="67954-267">Use the bracket symbols "[" and "]" to begin and end the list of values.</span></span>

 <span data-ttu-id="67954-268">In the following example, the expression evaluates to true if the value of user.department equals any of the values in the list:</span><span class="sxs-lookup"><span data-stu-id="67954-268">In the following example, the expression evaluates to true if the value of user.department equals any of the values in the list:</span></span>

```
   user.department -In ["50001","50002","50003",“50005”,“50006”,“50007”,“50008”,“50016”,“50020”,“50024”,“50038”,“50039”,“51100”]
```

## <a name="supported-values"></a><span data-ttu-id="67954-269">Supported values</span><span class="sxs-lookup"><span data-stu-id="67954-269">Supported values</span></span>

<span data-ttu-id="67954-270">The values used in an expression can consist of several types, including:</span><span class="sxs-lookup"><span data-stu-id="67954-270">The values used in an expression can consist of several types, including:</span></span>

* <span data-ttu-id="67954-271">Strings</span><span class="sxs-lookup"><span data-stu-id="67954-271">Strings</span></span>
* <span data-ttu-id="67954-272">Boolean – true, false</span><span class="sxs-lookup"><span data-stu-id="67954-272">Boolean – true, false</span></span>
* <span data-ttu-id="67954-273">Numbers</span><span class="sxs-lookup"><span data-stu-id="67954-273">Numbers</span></span>
* <span data-ttu-id="67954-274">Arrays – number array, string array</span><span class="sxs-lookup"><span data-stu-id="67954-274">Arrays – number array, string array</span></span>

<span data-ttu-id="67954-275">When specifying a value within an expression it is important to use the correct syntax to avoid errors.</span><span class="sxs-lookup"><span data-stu-id="67954-275">When specifying a value within an expression it is important to use the correct syntax to avoid errors.</span></span> <span data-ttu-id="67954-276">Some syntax tips are:</span><span class="sxs-lookup"><span data-stu-id="67954-276">Some syntax tips are:</span></span>

* <span data-ttu-id="67954-277">Double quotes are optional unless the value is a string.</span><span class="sxs-lookup"><span data-stu-id="67954-277">Double quotes are optional unless the value is a string.</span></span>
* <span data-ttu-id="67954-278">String and regex operations are not case sensitive.</span><span class="sxs-lookup"><span data-stu-id="67954-278">String and regex operations are not case sensitive.</span></span>
* <span data-ttu-id="67954-279">When a string value contains double quotes, both quotes should be escaped using the \` character, for example, user.department -eq \`"Sales\`" is the proper syntax when "Sales" is the value.</span><span class="sxs-lookup"><span data-stu-id="67954-279">When a string value contains double quotes, both quotes should be escaped using the \` character, for example, user.department -eq \`"Sales\`" is the proper syntax when "Sales" is the value.</span></span>
* <span data-ttu-id="67954-280">You can also perform Null checks, using null as a value, for example, `user.department -eq null`.</span><span class="sxs-lookup"><span data-stu-id="67954-280">You can also perform Null checks, using null as a value, for example, `user.department -eq null`.</span></span>

### <a name="use-of-null-values"></a><span data-ttu-id="67954-281">Use of Null values</span><span class="sxs-lookup"><span data-stu-id="67954-281">Use of Null values</span></span>

<span data-ttu-id="67954-282">To specify a null value in a rule, you can use the *null* value.</span><span class="sxs-lookup"><span data-stu-id="67954-282">To specify a null value in a rule, you can use the *null* value.</span></span> 

* <span data-ttu-id="67954-283">Use -eq or -ne when comparing the *null* value in an expression.</span><span class="sxs-lookup"><span data-stu-id="67954-283">Use -eq or -ne when comparing the *null* value in an expression.</span></span>
* <span data-ttu-id="67954-284">Use quotes around the word *null* only if you want it to be interpreted as a literal string value.</span><span class="sxs-lookup"><span data-stu-id="67954-284">Use quotes around the word *null* only if you want it to be interpreted as a literal string value.</span></span>
* <span data-ttu-id="67954-285">The -not operator can't be used as a comparative operator for null.</span><span class="sxs-lookup"><span data-stu-id="67954-285">The -not operator can't be used as a comparative operator for null.</span></span> <span data-ttu-id="67954-286">If you use it, you get an error whether you use null or $null.</span><span class="sxs-lookup"><span data-stu-id="67954-286">If you use it, you get an error whether you use null or $null.</span></span>

<span data-ttu-id="67954-287">The correct way to reference the null value is as follows:</span><span class="sxs-lookup"><span data-stu-id="67954-287">The correct way to reference the null value is as follows:</span></span>

```
   user.mail –ne null
```

## <a name="rules-with-multiple-expressions"></a><span data-ttu-id="67954-288">Rules with multiple expressions</span><span class="sxs-lookup"><span data-stu-id="67954-288">Rules with multiple expressions</span></span>

<span data-ttu-id="67954-289">A group membership rule can consist of more than one single expression connected by the -and, -or, and -not logical operators.</span><span class="sxs-lookup"><span data-stu-id="67954-289">A group membership rule can consist of more than one single expression connected by the -and, -or, and -not logical operators.</span></span> <span data-ttu-id="67954-290">Logical operators can also be used in combination.</span><span class="sxs-lookup"><span data-stu-id="67954-290">Logical operators can also be used in combination.</span></span> 

<span data-ttu-id="67954-291">The following are examples of properly constructed membership rules with multiple expressions:</span><span class="sxs-lookup"><span data-stu-id="67954-291">The following are examples of properly constructed membership rules with multiple expressions:</span></span>

```
(user.department -eq "Sales") -or (user.department -eq "Marketing")
(user.department -eq "Sales") -and -not (user.jobTitle -contains "SDE")
```

### <a name="operator-precedence"></a><span data-ttu-id="67954-292">Operator precedence</span><span class="sxs-lookup"><span data-stu-id="67954-292">Operator precedence</span></span>

<span data-ttu-id="67954-293">All operators are listed below in order of precedence from highest to lowest.</span><span class="sxs-lookup"><span data-stu-id="67954-293">All operators are listed below in order of precedence from highest to lowest.</span></span> <span data-ttu-id="67954-294">Operators on same line are of equal precedence:</span><span class="sxs-lookup"><span data-stu-id="67954-294">Operators on same line are of equal precedence:</span></span>

```
-eq -ne -startsWith -notStartsWith -contains -notContains -match –notMatch -in -notIn
-not
-and
-or
-any -all
```

<span data-ttu-id="67954-295">The following is an example of operator precedence where two expressions are being evaluated for the user:</span><span class="sxs-lookup"><span data-stu-id="67954-295">The following is an example of operator precedence where two expressions are being evaluated for the user:</span></span>

```
   user.department –eq "Marketing" –and user.country –eq "US"
```

<span data-ttu-id="67954-296">Parentheses are needed only when precedence does not meet your requirements.</span><span class="sxs-lookup"><span data-stu-id="67954-296">Parentheses are needed only when precedence does not meet your requirements.</span></span> <span data-ttu-id="67954-297">For example, if you want department to be evaluated first, the following shows how parentheses can be used to determine order:</span><span class="sxs-lookup"><span data-stu-id="67954-297">For example, if you want department to be evaluated first, the following shows how parentheses can be used to determine order:</span></span>

```
   user.country –eq "US" –and (user.department –eq "Marketing" –or user.department –eq "Sales")
```

## <a name="rules-with-complex-expressions"></a><span data-ttu-id="67954-298">Rules with complex expressions</span><span class="sxs-lookup"><span data-stu-id="67954-298">Rules with complex expressions</span></span>

<span data-ttu-id="67954-299">A membership rule can consist of complex expressions where the properties, operators, and values take on more complex forms.</span><span class="sxs-lookup"><span data-stu-id="67954-299">A membership rule can consist of complex expressions where the properties, operators, and values take on more complex forms.</span></span> <span data-ttu-id="67954-300">Expressions are considered complex when any of the following are true:</span><span class="sxs-lookup"><span data-stu-id="67954-300">Expressions are considered complex when any of the following are true:</span></span>

* <span data-ttu-id="67954-301">The property consists of a collection of values; specifically, multi-valued properties</span><span class="sxs-lookup"><span data-stu-id="67954-301">The property consists of a collection of values; specifically, multi-valued properties</span></span>
* <span data-ttu-id="67954-302">The expressions use the -any and -all operators</span><span class="sxs-lookup"><span data-stu-id="67954-302">The expressions use the -any and -all operators</span></span>
* <span data-ttu-id="67954-303">The value of the expression can itself be one or more expressions</span><span class="sxs-lookup"><span data-stu-id="67954-303">The value of the expression can itself be one or more expressions</span></span>

## <a name="multi-value-properties"></a><span data-ttu-id="67954-304">Multi-value properties</span><span class="sxs-lookup"><span data-stu-id="67954-304">Multi-value properties</span></span>

<span data-ttu-id="67954-305">Multi-value properties are collections of objects of the same type.</span><span class="sxs-lookup"><span data-stu-id="67954-305">Multi-value properties are collections of objects of the same type.</span></span> <span data-ttu-id="67954-306">They can be used to create membership rules using the -any and -all logical operators.</span><span class="sxs-lookup"><span data-stu-id="67954-306">They can be used to create membership rules using the -any and -all logical operators.</span></span>

| <span data-ttu-id="67954-307">Properties</span><span class="sxs-lookup"><span data-stu-id="67954-307">Properties</span></span> | <span data-ttu-id="67954-308">Values</span><span class="sxs-lookup"><span data-stu-id="67954-308">Values</span></span> | <span data-ttu-id="67954-309">Usage</span><span class="sxs-lookup"><span data-stu-id="67954-309">Usage</span></span> |
| --- | --- | --- |
| <span data-ttu-id="67954-310">assignedPlans</span><span class="sxs-lookup"><span data-stu-id="67954-310">assignedPlans</span></span> | <span data-ttu-id="67954-311">Each object in the collection exposes the following string properties: capabilityStatus, service, servicePlanId</span><span class="sxs-lookup"><span data-stu-id="67954-311">Each object in the collection exposes the following string properties: capabilityStatus, service, servicePlanId</span></span> |<span data-ttu-id="67954-312">user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")</span><span class="sxs-lookup"><span data-stu-id="67954-312">user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")</span></span> |
| <span data-ttu-id="67954-313">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="67954-313">proxyAddresses</span></span>| <span data-ttu-id="67954-314">SMTP: alias@domain smtp: alias@domain</span><span class="sxs-lookup"><span data-stu-id="67954-314">SMTP: alias@domain smtp: alias@domain</span></span> | <span data-ttu-id="67954-315">(user.proxyAddresses -any (\_ -contains "contoso"))</span><span class="sxs-lookup"><span data-stu-id="67954-315">(user.proxyAddresses -any (\_ -contains "contoso"))</span></span> |

### <a name="using-the--any-and--all-operators"></a><span data-ttu-id="67954-316">Using the -any and -all operators</span><span class="sxs-lookup"><span data-stu-id="67954-316">Using the -any and -all operators</span></span>

<span data-ttu-id="67954-317">You can use -any and -all operators to apply a condition to one or all of the items in the collection, respectively.</span><span class="sxs-lookup"><span data-stu-id="67954-317">You can use -any and -all operators to apply a condition to one or all of the items in the collection, respectively.</span></span>

* <span data-ttu-id="67954-318">-any (satisfied when at least one item in the collection matches the condition)</span><span class="sxs-lookup"><span data-stu-id="67954-318">-any (satisfied when at least one item in the collection matches the condition)</span></span>
* <span data-ttu-id="67954-319">-all (satisfied when all items in the collection match the condition)</span><span class="sxs-lookup"><span data-stu-id="67954-319">-all (satisfied when all items in the collection match the condition)</span></span>

#### <a name="example-1"></a><span data-ttu-id="67954-320">Example 1</span><span class="sxs-lookup"><span data-stu-id="67954-320">Example 1</span></span>

<span data-ttu-id="67954-321">assignedPlans is a multi-value property that lists all service plans assigned to the user.</span><span class="sxs-lookup"><span data-stu-id="67954-321">assignedPlans is a multi-value property that lists all service plans assigned to the user.</span></span> <span data-ttu-id="67954-322">The following expression selects users who have the Exchange Online (Plan 2) service plan (as a GUID value) that is also in Enabled state:</span><span class="sxs-lookup"><span data-stu-id="67954-322">The following expression selects users who have the Exchange Online (Plan 2) service plan (as a GUID value) that is also in Enabled state:</span></span>

```
user.assignedPlans -any (assignedPlan.servicePlanId -eq "efb87545-963c-4e0d-99df-69c6916d9eb0" -and assignedPlan.capabilityStatus -eq "Enabled")
```

<span data-ttu-id="67954-323">A rule such as this one can be used to group all users for whom an Office 365 (or other Microsoft Online Service) capability is enabled.</span><span class="sxs-lookup"><span data-stu-id="67954-323">A rule such as this one can be used to group all users for whom an Office 365 (or other Microsoft Online Service) capability is enabled.</span></span> <span data-ttu-id="67954-324">You could then apply with a set of policies to the group.</span><span class="sxs-lookup"><span data-stu-id="67954-324">You could then apply with a set of policies to the group.</span></span>

#### <a name="example-2"></a><span data-ttu-id="67954-325">Example 2</span><span class="sxs-lookup"><span data-stu-id="67954-325">Example 2</span></span>

<span data-ttu-id="67954-326">The following expression selects all users who have any service plan that is associated with the Intune service (identified by service name "SCO"):</span><span class="sxs-lookup"><span data-stu-id="67954-326">The following expression selects all users who have any service plan that is associated with the Intune service (identified by service name "SCO"):</span></span>

```
user.assignedPlans -any (assignedPlan.service -eq "SCO" -and assignedPlan.capabilityStatus -eq "Enabled")
```

### <a name="using-the-underscore--syntax"></a><span data-ttu-id="67954-327">Using the underscore (\_) syntax</span><span class="sxs-lookup"><span data-stu-id="67954-327">Using the underscore (\_) syntax</span></span>

<span data-ttu-id="67954-328">The underscore (\_) syntax matches occurrences of a specific value in one of the multivalued string collection properties to add users or devices to a dynamic group.</span><span class="sxs-lookup"><span data-stu-id="67954-328">The underscore (\_) syntax matches occurrences of a specific value in one of the multivalued string collection properties to add users or devices to a dynamic group.</span></span> <span data-ttu-id="67954-329">It is used with the -any or -all operators.</span><span class="sxs-lookup"><span data-stu-id="67954-329">It is used with the -any or -all operators.</span></span>

<span data-ttu-id="67954-330">Here's an example of using the underscore (\_) in a rule to add members based on user.proxyAddress (it works the same for user.otherMails).</span><span class="sxs-lookup"><span data-stu-id="67954-330">Here's an example of using the underscore (\_) in a rule to add members based on user.proxyAddress (it works the same for user.otherMails).</span></span> <span data-ttu-id="67954-331">This rule adds any user with proxy address that contains "contoso" to the group.</span><span class="sxs-lookup"><span data-stu-id="67954-331">This rule adds any user with proxy address that contains "contoso" to the group.</span></span>

```
(user.proxyAddresses -any (_ -contains "contoso"))
```

## <a name="other-properties-and-common-rules"></a><span data-ttu-id="67954-332">Other properties and common rules</span><span class="sxs-lookup"><span data-stu-id="67954-332">Other properties and common rules</span></span>

### <a name="create-a-direct-reports-rule"></a><span data-ttu-id="67954-333">Create a "Direct reports" rule</span><span class="sxs-lookup"><span data-stu-id="67954-333">Create a "Direct reports" rule</span></span>

<span data-ttu-id="67954-334">You can create a group containing all direct reports of a manager.</span><span class="sxs-lookup"><span data-stu-id="67954-334">You can create a group containing all direct reports of a manager.</span></span> <span data-ttu-id="67954-335">When the manager's direct reports change in the future, the group's membership is adjusted automatically.</span><span class="sxs-lookup"><span data-stu-id="67954-335">When the manager's direct reports change in the future, the group's membership is adjusted automatically.</span></span>

<span data-ttu-id="67954-336">The direct reports rule is constructed using the following syntax:</span><span class="sxs-lookup"><span data-stu-id="67954-336">The direct reports rule is constructed using the following syntax:</span></span>

```
Direct Reports for "{objectID_of_manager}"
```

<span data-ttu-id="67954-337">Here's an example of a valid rule where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is the objectID of the manager:</span><span class="sxs-lookup"><span data-stu-id="67954-337">Here's an example of a valid rule where “62e19b97-8b3d-4d4a-a106-4ce66896a863” is the objectID of the manager:</span></span>

```
Direct Reports for "62e19b97-8b3d-4d4a-a106-4ce66896a863"
```

<span data-ttu-id="67954-338">The following tips can help you use the rule properly.</span><span class="sxs-lookup"><span data-stu-id="67954-338">The following tips can help you use the rule properly.</span></span>

* <span data-ttu-id="67954-339">The **Manager ID** is the object ID of the manager.</span><span class="sxs-lookup"><span data-stu-id="67954-339">The **Manager ID** is the object ID of the manager.</span></span> <span data-ttu-id="67954-340">It can be found in the manager's **Profile**.</span><span class="sxs-lookup"><span data-stu-id="67954-340">It can be found in the manager's **Profile**.</span></span>
* <span data-ttu-id="67954-341">For the rule to work, make sure the **Manager** property is set correctly for users in your tenant.</span><span class="sxs-lookup"><span data-stu-id="67954-341">For the rule to work, make sure the **Manager** property is set correctly for users in your tenant.</span></span> <span data-ttu-id="67954-342">You can check the current value in the user's **Profile**.</span><span class="sxs-lookup"><span data-stu-id="67954-342">You can check the current value in the user's **Profile**.</span></span>
* <span data-ttu-id="67954-343">This rule supports only the manager's direct reports.</span><span class="sxs-lookup"><span data-stu-id="67954-343">This rule supports only the manager's direct reports.</span></span> <span data-ttu-id="67954-344">In other words, you can't create a group with the manager's direct reports *and* their reports.</span><span class="sxs-lookup"><span data-stu-id="67954-344">In other words, you can't create a group with the manager's direct reports *and* their reports.</span></span>
* <span data-ttu-id="67954-345">This rule can't be combined with any other membership rules.</span><span class="sxs-lookup"><span data-stu-id="67954-345">This rule can't be combined with any other membership rules.</span></span>

### <a name="create-an-all-users-rule"></a><span data-ttu-id="67954-346">Create an "All users" rule</span><span class="sxs-lookup"><span data-stu-id="67954-346">Create an "All users" rule</span></span>

<span data-ttu-id="67954-347">You can create a group containing all users within a tenant using a membership rule.</span><span class="sxs-lookup"><span data-stu-id="67954-347">You can create a group containing all users within a tenant using a membership rule.</span></span> <span data-ttu-id="67954-348">When users are added or removed from the tenant in the future, the group's membership is adjusted automatically.</span><span class="sxs-lookup"><span data-stu-id="67954-348">When users are added or removed from the tenant in the future, the group's membership is adjusted automatically.</span></span>

<span data-ttu-id="67954-349">The “All users” rule is constructed using single expression using the -ne operator and the null value.</span><span class="sxs-lookup"><span data-stu-id="67954-349">The “All users” rule is constructed using single expression using the -ne operator and the null value.</span></span> <span data-ttu-id="67954-350">This rule adds B2B guest users as well as member users to the group.</span><span class="sxs-lookup"><span data-stu-id="67954-350">This rule adds B2B guest users as well as member users to the group.</span></span>

```
user.objectid -ne null
```

### <a name="create-an-all-devices-rule"></a><span data-ttu-id="67954-351">Create an “All devices” rule</span><span class="sxs-lookup"><span data-stu-id="67954-351">Create an “All devices” rule</span></span>

<span data-ttu-id="67954-352">You can create a group containing all devices within a tenant using a membership rule.</span><span class="sxs-lookup"><span data-stu-id="67954-352">You can create a group containing all devices within a tenant using a membership rule.</span></span> <span data-ttu-id="67954-353">When devices are added or removed from the tenant in the future, the group's membership is adjusted automatically.</span><span class="sxs-lookup"><span data-stu-id="67954-353">When devices are added or removed from the tenant in the future, the group's membership is adjusted automatically.</span></span>

<span data-ttu-id="67954-354">The “All Devices” rule is constructed using single expression using the -ne operator and the null value:</span><span class="sxs-lookup"><span data-stu-id="67954-354">The “All Devices” rule is constructed using single expression using the -ne operator and the null value:</span></span>

```
device.objectid -ne null
```

### <a name="extension-properties-and-custom-extension-properties"></a><span data-ttu-id="67954-355">Extension properties and custom extension properties</span><span class="sxs-lookup"><span data-stu-id="67954-355">Extension properties and custom extension properties</span></span>

<span data-ttu-id="67954-356">Extension attributes and custom extenson properties are supported as string properties in dynamic membership rules.</span><span class="sxs-lookup"><span data-stu-id="67954-356">Extension attributes and custom extenson properties are supported as string properties in dynamic membership rules.</span></span> <span data-ttu-id="67954-357">Extension attributes are synced from on-premises Window Server AD and take the format of "ExtensionAttributeX", where X equals 1 - 15.</span><span class="sxs-lookup"><span data-stu-id="67954-357">Extension attributes are synced from on-premises Window Server AD and take the format of "ExtensionAttributeX", where X equals 1 - 15.</span></span> <span data-ttu-id="67954-358">Here's an example of a rule that uses an extension attribute as a property:</span><span class="sxs-lookup"><span data-stu-id="67954-358">Here's an example of a rule that uses an extension attribute as a property:</span></span>

```
(user.extensionAttribute15 -eq "Marketing")
```

<span data-ttu-id="67954-359">Custom extension properties are synced from on-premises Windows Server AD or from a connected SaaS application and are of the format of `user.extension_[GUID]__[Attribute]`, where:</span><span class="sxs-lookup"><span data-stu-id="67954-359">Custom extension properties are synced from on-premises Windows Server AD or from a connected SaaS application and are of the format of `user.extension_[GUID]__[Attribute]`, where:</span></span>

* <span data-ttu-id="67954-360">[GUID] is the unique identifier in Azure AD for the application that created the property in Azure AD</span><span class="sxs-lookup"><span data-stu-id="67954-360">[GUID] is the unique identifier in Azure AD for the application that created the property in Azure AD</span></span>
* <span data-ttu-id="67954-361">[Attribute] is the name of the property as it was created</span><span class="sxs-lookup"><span data-stu-id="67954-361">[Attribute] is the name of the property as it was created</span></span>

<span data-ttu-id="67954-362">An example of a rule that uses a custom extension property is:</span><span class="sxs-lookup"><span data-stu-id="67954-362">An example of a rule that uses a custom extension property is:</span></span>

```
user.extension_c272a57b722d4eb29bfe327874ae79cb__OfficeNumber -eq "123"
```

<span data-ttu-id="67954-363">The custom property name can be found in the directory by querying a user's property using Graph Explorer and searching for the property name.</span><span class="sxs-lookup"><span data-stu-id="67954-363">The custom property name can be found in the directory by querying a user's property using Graph Explorer and searching for the property name.</span></span>

## <a name="rules-for-devices"></a><span data-ttu-id="67954-364">Rules for devices</span><span class="sxs-lookup"><span data-stu-id="67954-364">Rules for devices</span></span>

<span data-ttu-id="67954-365">You can also create a rule that selects device objects for membership in a group.</span><span class="sxs-lookup"><span data-stu-id="67954-365">You can also create a rule that selects device objects for membership in a group.</span></span> <span data-ttu-id="67954-366">You can't have both users and devices as group members.</span><span class="sxs-lookup"><span data-stu-id="67954-366">You can't have both users and devices as group members.</span></span> <span data-ttu-id="67954-367">The following device attributes can be used.</span><span class="sxs-lookup"><span data-stu-id="67954-367">The following device attributes can be used.</span></span>

 <span data-ttu-id="67954-368">Device attribute</span><span class="sxs-lookup"><span data-stu-id="67954-368">Device attribute</span></span>  | <span data-ttu-id="67954-369">Values</span><span class="sxs-lookup"><span data-stu-id="67954-369">Values</span></span> | <span data-ttu-id="67954-370">Example</span><span class="sxs-lookup"><span data-stu-id="67954-370">Example</span></span>
 ----- | ----- | ----------------
 <span data-ttu-id="67954-371">accountEnabled</span><span class="sxs-lookup"><span data-stu-id="67954-371">accountEnabled</span></span> | <span data-ttu-id="67954-372">true false</span><span class="sxs-lookup"><span data-stu-id="67954-372">true false</span></span> | <span data-ttu-id="67954-373">(device.accountEnabled -eq true)</span><span class="sxs-lookup"><span data-stu-id="67954-373">(device.accountEnabled -eq true)</span></span>
 <span data-ttu-id="67954-374">displayName</span><span class="sxs-lookup"><span data-stu-id="67954-374">displayName</span></span> | <span data-ttu-id="67954-375">any string value</span><span class="sxs-lookup"><span data-stu-id="67954-375">any string value</span></span> |<span data-ttu-id="67954-376">(device.displayName -eq "Rob Iphone”)</span><span class="sxs-lookup"><span data-stu-id="67954-376">(device.displayName -eq "Rob Iphone”)</span></span>
 <span data-ttu-id="67954-377">deviceOSType</span><span class="sxs-lookup"><span data-stu-id="67954-377">deviceOSType</span></span> | <span data-ttu-id="67954-378">any string value</span><span class="sxs-lookup"><span data-stu-id="67954-378">any string value</span></span> | <span data-ttu-id="67954-379">(device.deviceOSType -eq "iPad") -or (device.deviceOSType -eq "iPhone")</span><span class="sxs-lookup"><span data-stu-id="67954-379">(device.deviceOSType -eq "iPad") -or (device.deviceOSType -eq "iPhone")</span></span>
 <span data-ttu-id="67954-380">deviceOSVersion</span><span class="sxs-lookup"><span data-stu-id="67954-380">deviceOSVersion</span></span> | <span data-ttu-id="67954-381">any string value</span><span class="sxs-lookup"><span data-stu-id="67954-381">any string value</span></span> | <span data-ttu-id="67954-382">(device.OSVersion -eq "9.1")</span><span class="sxs-lookup"><span data-stu-id="67954-382">(device.OSVersion -eq "9.1")</span></span>
 <span data-ttu-id="67954-383">deviceCategory</span><span class="sxs-lookup"><span data-stu-id="67954-383">deviceCategory</span></span> | <span data-ttu-id="67954-384">a valid device category name</span><span class="sxs-lookup"><span data-stu-id="67954-384">a valid device category name</span></span> | <span data-ttu-id="67954-385">(device.deviceCategory -eq "BYOD")</span><span class="sxs-lookup"><span data-stu-id="67954-385">(device.deviceCategory -eq "BYOD")</span></span>
 <span data-ttu-id="67954-386">deviceManufacturer</span><span class="sxs-lookup"><span data-stu-id="67954-386">deviceManufacturer</span></span> | <span data-ttu-id="67954-387">any string value</span><span class="sxs-lookup"><span data-stu-id="67954-387">any string value</span></span> | <span data-ttu-id="67954-388">(device.deviceManufacturer -eq "Samsung")</span><span class="sxs-lookup"><span data-stu-id="67954-388">(device.deviceManufacturer -eq "Samsung")</span></span>
 <span data-ttu-id="67954-389">deviceModel</span><span class="sxs-lookup"><span data-stu-id="67954-389">deviceModel</span></span> | <span data-ttu-id="67954-390">any string value</span><span class="sxs-lookup"><span data-stu-id="67954-390">any string value</span></span> | <span data-ttu-id="67954-391">(device.deviceModel -eq "iPad Air")</span><span class="sxs-lookup"><span data-stu-id="67954-391">(device.deviceModel -eq "iPad Air")</span></span>
 <span data-ttu-id="67954-392">deviceOwnership</span><span class="sxs-lookup"><span data-stu-id="67954-392">deviceOwnership</span></span> | <span data-ttu-id="67954-393">Personal, Company, Unknown</span><span class="sxs-lookup"><span data-stu-id="67954-393">Personal, Company, Unknown</span></span> | <span data-ttu-id="67954-394">(device.deviceOwnership -eq "Company")</span><span class="sxs-lookup"><span data-stu-id="67954-394">(device.deviceOwnership -eq "Company")</span></span>
 <span data-ttu-id="67954-395">domainName</span><span class="sxs-lookup"><span data-stu-id="67954-395">domainName</span></span> | <span data-ttu-id="67954-396">any string value</span><span class="sxs-lookup"><span data-stu-id="67954-396">any string value</span></span> | <span data-ttu-id="67954-397">(device.domainName -eq "contoso.com")</span><span class="sxs-lookup"><span data-stu-id="67954-397">(device.domainName -eq "contoso.com")</span></span>
 <span data-ttu-id="67954-398">enrollmentProfileName</span><span class="sxs-lookup"><span data-stu-id="67954-398">enrollmentProfileName</span></span> | <span data-ttu-id="67954-399">Apple Device Enrollment Profile or Windows Autopilot profile name</span><span class="sxs-lookup"><span data-stu-id="67954-399">Apple Device Enrollment Profile or Windows Autopilot profile name</span></span> | <span data-ttu-id="67954-400">(device.enrollmentProfileName -eq "DEP iPhones")</span><span class="sxs-lookup"><span data-stu-id="67954-400">(device.enrollmentProfileName -eq "DEP iPhones")</span></span>
 <span data-ttu-id="67954-401">isRooted</span><span class="sxs-lookup"><span data-stu-id="67954-401">isRooted</span></span> | <span data-ttu-id="67954-402">true false</span><span class="sxs-lookup"><span data-stu-id="67954-402">true false</span></span> | <span data-ttu-id="67954-403">(device.isRooted -eq true)</span><span class="sxs-lookup"><span data-stu-id="67954-403">(device.isRooted -eq true)</span></span>
 <span data-ttu-id="67954-404">managementType</span><span class="sxs-lookup"><span data-stu-id="67954-404">managementType</span></span> | <span data-ttu-id="67954-405">MDM (for mobile devices)</span><span class="sxs-lookup"><span data-stu-id="67954-405">MDM (for mobile devices)</span></span><br><span data-ttu-id="67954-406">PC (for computers managed by the Intune PC agent)</span><span class="sxs-lookup"><span data-stu-id="67954-406">PC (for computers managed by the Intune PC agent)</span></span> | <span data-ttu-id="67954-407">(device.managementType -eq "MDM")</span><span class="sxs-lookup"><span data-stu-id="67954-407">(device.managementType -eq "MDM")</span></span>
 <span data-ttu-id="67954-408">organizationalUnit</span><span class="sxs-lookup"><span data-stu-id="67954-408">organizationalUnit</span></span> | <span data-ttu-id="67954-409">any string value matching the name of the organizational unit set by an on-premises Active Directory</span><span class="sxs-lookup"><span data-stu-id="67954-409">any string value matching the name of the organizational unit set by an on-premises Active Directory</span></span> | <span data-ttu-id="67954-410">(device.organizationalUnit -eq "US PCs")</span><span class="sxs-lookup"><span data-stu-id="67954-410">(device.organizationalUnit -eq "US PCs")</span></span>
 <span data-ttu-id="67954-411">deviceId</span><span class="sxs-lookup"><span data-stu-id="67954-411">deviceId</span></span> | <span data-ttu-id="67954-412">a valid Azure AD device ID</span><span class="sxs-lookup"><span data-stu-id="67954-412">a valid Azure AD device ID</span></span> | <span data-ttu-id="67954-413">(device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")</span><span class="sxs-lookup"><span data-stu-id="67954-413">(device.deviceId -eq "d4fe7726-5966-431c-b3b8-cddc8fdb717d")</span></span>
 <span data-ttu-id="67954-414">objectId</span><span class="sxs-lookup"><span data-stu-id="67954-414">objectId</span></span> | <span data-ttu-id="67954-415">a valid Azure AD object ID</span><span class="sxs-lookup"><span data-stu-id="67954-415">a valid Azure AD object ID</span></span> |  <span data-ttu-id="67954-416">(device.objectId -eq 76ad43c9-32c5-45e8-a272-7b58b58f596d")</span><span class="sxs-lookup"><span data-stu-id="67954-416">(device.objectId -eq 76ad43c9-32c5-45e8-a272-7b58b58f596d")</span></span>

## <a name="next-steps"></a><span data-ttu-id="67954-417">Next steps</span><span class="sxs-lookup"><span data-stu-id="67954-417">Next steps</span></span>

<span data-ttu-id="67954-418">These articles provide additional information on groups in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="67954-418">These articles provide additional information on groups in Azure Active Directory.</span></span>

* [<span data-ttu-id="67954-419">See existing groups</span><span class="sxs-lookup"><span data-stu-id="67954-419">See existing groups</span></span>](../fundamentals/active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="67954-420">Create a new group and adding members</span><span class="sxs-lookup"><span data-stu-id="67954-420">Create a new group and adding members</span></span>](../fundamentals/active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="67954-421">Manage settings of a group</span><span class="sxs-lookup"><span data-stu-id="67954-421">Manage settings of a group</span></span>](../fundamentals/active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="67954-422">Manage memberships of a group</span><span class="sxs-lookup"><span data-stu-id="67954-422">Manage memberships of a group</span></span>](../fundamentals/active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="67954-423">Manage dynamic rules for users in a group</span><span class="sxs-lookup"><span data-stu-id="67954-423">Manage dynamic rules for users in a group</span></span>](groups-dynamic-membership.md)
