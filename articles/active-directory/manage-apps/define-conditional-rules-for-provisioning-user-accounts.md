---
title: Provision apps with scoping filters | Microsoft Docs
description: Learn how to use scoping filters to prevent objects in apps that support automated user provisioning from being provisioned if an object doesn't satisfy your business requirements.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/09/2018
ms.author: barbkess
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 17e9616b39491aac01427ee34fb23db556c5c9b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969102"
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="2a46c-103">Attribute-based application provisioning with scoping filters</span><span class="sxs-lookup"><span data-stu-id="2a46c-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="2a46c-104">The objective of this article is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to an application.</span><span class="sxs-lookup"><span data-stu-id="2a46c-104">The objective of this article is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to an application.</span></span>

## <a name="scoping-filter-use-cases"></a><span data-ttu-id="2a46c-105">Scoping filter use cases</span><span class="sxs-lookup"><span data-stu-id="2a46c-105">Scoping filter use cases</span></span>

<span data-ttu-id="2a46c-106">A scoping filter allows the Azure Active Directory (Azure AD) provisioning service to include or exclude any users who have an attribute that matches a specific value.</span><span class="sxs-lookup"><span data-stu-id="2a46c-106">A scoping filter allows the Azure Active Directory (Azure AD) provisioning service to include or exclude any users who have an attribute that matches a specific value.</span></span> <span data-ttu-id="2a46c-107">For example, when provisioning users from Azure AD to a SaaS application used by a sales team, you can specify that only users with a "Department" attribute of "Sales" should be in scope for provisioning.</span><span class="sxs-lookup"><span data-stu-id="2a46c-107">For example, when provisioning users from Azure AD to a SaaS application used by a sales team, you can specify that only users with a "Department" attribute of "Sales" should be in scope for provisioning.</span></span>

<span data-ttu-id="2a46c-108">Scoping filters can be used differently depending on the type of provisioning connector:</span><span class="sxs-lookup"><span data-stu-id="2a46c-108">Scoping filters can be used differently depending on the type of provisioning connector:</span></span>

* <span data-ttu-id="2a46c-109">**Outbound provisioning from Azure AD to SaaS applications**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-109">**Outbound provisioning from Azure AD to SaaS applications**.</span></span> <span data-ttu-id="2a46c-110">When Azure AD is the source system, [user and group assignments](assign-user-or-group-access-portal.md) are the most common method for determining which users are in scope for provisioning.</span><span class="sxs-lookup"><span data-stu-id="2a46c-110">When Azure AD is the source system, [user and group assignments](assign-user-or-group-access-portal.md) are the most common method for determining which users are in scope for provisioning.</span></span> <span data-ttu-id="2a46c-111">These assignments also are used for enabling single sign-on and provide a single method to manage access and provisioning.</span><span class="sxs-lookup"><span data-stu-id="2a46c-111">These assignments also are used for enabling single sign-on and provide a single method to manage access and provisioning.</span></span> <span data-ttu-id="2a46c-112">Scoping filters can be used optionally, in addition to assignments or instead of them, to filter users based on attribute values.</span><span class="sxs-lookup"><span data-stu-id="2a46c-112">Scoping filters can be used optionally, in addition to assignments or instead of them, to filter users based on attribute values.</span></span>

    >[!TIP]
    > <span data-ttu-id="2a46c-113">You can disable provisioning based on assignments for an enterprise application by changing settings in the [Scope](user-provisioning.md#how-do-i-set-up-automatic-provisioning-to-an-application) menu under the provisioning settings to **Sync all users and groups**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-113">You can disable provisioning based on assignments for an enterprise application by changing settings in the [Scope](user-provisioning.md#how-do-i-set-up-automatic-provisioning-to-an-application) menu under the provisioning settings to **Sync all users and groups**.</span></span> <span data-ttu-id="2a46c-114">Using this option plus attribute-based scoping filters offers faster performance than using group-based assignments.</span><span class="sxs-lookup"><span data-stu-id="2a46c-114">Using this option plus attribute-based scoping filters offers faster performance than using group-based assignments.</span></span>  

* <span data-ttu-id="2a46c-115">**Inbound provisioning from HCM applications to Azure AD and Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-115">**Inbound provisioning from HCM applications to Azure AD and Active Directory**.</span></span> <span data-ttu-id="2a46c-116">When an [HCM application such as Workday](../saas-apps/workday-tutorial.md) is the source system, scoping filters are the primary method for determining which users should be provisioned from the HCM application to Active Directory or Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2a46c-116">When an [HCM application such as Workday](../saas-apps/workday-tutorial.md) is the source system, scoping filters are the primary method for determining which users should be provisioned from the HCM application to Active Directory or Azure AD.</span></span>

<span data-ttu-id="2a46c-117">By default, Azure AD provisioning connectors do not have any attribute-based scoping filters configured.</span><span class="sxs-lookup"><span data-stu-id="2a46c-117">By default, Azure AD provisioning connectors do not have any attribute-based scoping filters configured.</span></span> 

## <a name="scoping-filter-construction"></a><span data-ttu-id="2a46c-118">Scoping filter construction</span><span class="sxs-lookup"><span data-stu-id="2a46c-118">Scoping filter construction</span></span>

<span data-ttu-id="2a46c-119">A scoping filter consists of one or more *clauses*.</span><span class="sxs-lookup"><span data-stu-id="2a46c-119">A scoping filter consists of one or more *clauses*.</span></span> <span data-ttu-id="2a46c-120">Clauses determine which users are allowed to pass through the scoping filter by evaluating each user's attributes.</span><span class="sxs-lookup"><span data-stu-id="2a46c-120">Clauses determine which users are allowed to pass through the scoping filter by evaluating each user's attributes.</span></span> <span data-ttu-id="2a46c-121">For example, you might have one clause that requires that a user's "State" attribute equals "New York", so only New York users are provisioned into the application.</span><span class="sxs-lookup"><span data-stu-id="2a46c-121">For example, you might have one clause that requires that a user's "State" attribute equals "New York", so only New York users are provisioned into the application.</span></span> 

<span data-ttu-id="2a46c-122">A single clause defines a single condition for a single attribute value.</span><span class="sxs-lookup"><span data-stu-id="2a46c-122">A single clause defines a single condition for a single attribute value.</span></span> <span data-ttu-id="2a46c-123">If multiple clauses are created in a single scoping filter, they're evaluated together by using "AND" logic.</span><span class="sxs-lookup"><span data-stu-id="2a46c-123">If multiple clauses are created in a single scoping filter, they're evaluated together by using "AND" logic.</span></span> <span data-ttu-id="2a46c-124">This means all clauses must evaluate to "true" in order for a user to be provisioned.</span><span class="sxs-lookup"><span data-stu-id="2a46c-124">This means all clauses must evaluate to "true" in order for a user to be provisioned.</span></span>

<span data-ttu-id="2a46c-125">Finally, multiple scoping filters can be created for a single application.</span><span class="sxs-lookup"><span data-stu-id="2a46c-125">Finally, multiple scoping filters can be created for a single application.</span></span> <span data-ttu-id="2a46c-126">If multiple scoping filters are present, they're evaluated together by using "OR" logic.</span><span class="sxs-lookup"><span data-stu-id="2a46c-126">If multiple scoping filters are present, they're evaluated together by using "OR" logic.</span></span> <span data-ttu-id="2a46c-127">This means that if all the clauses in any of the configured scoping filters evaluate to "true", the user is provisioned.</span><span class="sxs-lookup"><span data-stu-id="2a46c-127">This means that if all the clauses in any of the configured scoping filters evaluate to "true", the user is provisioned.</span></span>

<span data-ttu-id="2a46c-128">Each user or group processed by the Azure AD provisioning service is always evaluated individually against each scoping filter.</span><span class="sxs-lookup"><span data-stu-id="2a46c-128">Each user or group processed by the Azure AD provisioning service is always evaluated individually against each scoping filter.</span></span>

<span data-ttu-id="2a46c-129">As an example, consider the following scoping filter:</span><span class="sxs-lookup"><span data-stu-id="2a46c-129">As an example, consider the following scoping filter:</span></span>

![Scoping filter](./media/define-conditional-rules-for-provisioning-user-accounts/scoping-filter.PNG) 

<span data-ttu-id="2a46c-131">According to this scoping filter, users must satisfy the following criteria to be provisioned:</span><span class="sxs-lookup"><span data-stu-id="2a46c-131">According to this scoping filter, users must satisfy the following criteria to be provisioned:</span></span>

* <span data-ttu-id="2a46c-132">They must be in New York.</span><span class="sxs-lookup"><span data-stu-id="2a46c-132">They must be in New York.</span></span>
* <span data-ttu-id="2a46c-133">They must work in the Engineering department.</span><span class="sxs-lookup"><span data-stu-id="2a46c-133">They must work in the Engineering department.</span></span>
* <span data-ttu-id="2a46c-134">Their company employee ID must be between 1,000,000 and 2,000,000.</span><span class="sxs-lookup"><span data-stu-id="2a46c-134">Their company employee ID must be between 1,000,000 and 2,000,000.</span></span>
* <span data-ttu-id="2a46c-135">Their job title must not be null or empty.</span><span class="sxs-lookup"><span data-stu-id="2a46c-135">Their job title must not be null or empty.</span></span>

## <a name="create-scoping-filters"></a><span data-ttu-id="2a46c-136">Create scoping filters</span><span class="sxs-lookup"><span data-stu-id="2a46c-136">Create scoping filters</span></span>
<span data-ttu-id="2a46c-137">Scoping filters are configured as part of the attribute mappings for each Azure AD user provisioning connector.</span><span class="sxs-lookup"><span data-stu-id="2a46c-137">Scoping filters are configured as part of the attribute mappings for each Azure AD user provisioning connector.</span></span> <span data-ttu-id="2a46c-138">The following procedure assumes that you already set up automatic provisioning for [one of the supported applications](../saas-apps/tutorial-list.md) and are adding a scoping filter to it.</span><span class="sxs-lookup"><span data-stu-id="2a46c-138">The following procedure assumes that you already set up automatic provisioning for [one of the supported applications](../saas-apps/tutorial-list.md) and are adding a scoping filter to it.</span></span>

### <a name="create-a-scoping-filter"></a><span data-ttu-id="2a46c-139">Create a scoping filter</span><span class="sxs-lookup"><span data-stu-id="2a46c-139">Create a scoping filter</span></span>
1. <span data-ttu-id="2a46c-140">In the [Azure portal](https://portal.azure.com), go to the **Azure Active Directory** > **Enterprise Applications** > **All applications** section.</span><span class="sxs-lookup"><span data-stu-id="2a46c-140">In the [Azure portal](https://portal.azure.com), go to the **Azure Active Directory** > **Enterprise Applications** > **All applications** section.</span></span>

2. <span data-ttu-id="2a46c-141">Select the application for which you have configured automatic provisioning: for example, "ServiceNow".</span><span class="sxs-lookup"><span data-stu-id="2a46c-141">Select the application for which you have configured automatic provisioning: for example, "ServiceNow".</span></span>

3. <span data-ttu-id="2a46c-142">Select the **Provisioning** tab.</span><span class="sxs-lookup"><span data-stu-id="2a46c-142">Select the **Provisioning** tab.</span></span>

4. <span data-ttu-id="2a46c-143">In the **Mappings** section, select the mapping that you want to configure a scoping filter for: for example, "Synchronize Azure Active Directory Users to ServiceNow".</span><span class="sxs-lookup"><span data-stu-id="2a46c-143">In the **Mappings** section, select the mapping that you want to configure a scoping filter for: for example, "Synchronize Azure Active Directory Users to ServiceNow".</span></span>

5. <span data-ttu-id="2a46c-144">Select the **Source object scope** menu.</span><span class="sxs-lookup"><span data-stu-id="2a46c-144">Select the **Source object scope** menu.</span></span>

6. <span data-ttu-id="2a46c-145">Select **Add scoping filter**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-145">Select **Add scoping filter**.</span></span>

7. <span data-ttu-id="2a46c-146">Define a clause by selecting a source **Attribute Name**, an **Operator**, and an **Attribute Value** to match against.</span><span class="sxs-lookup"><span data-stu-id="2a46c-146">Define a clause by selecting a source **Attribute Name**, an **Operator**, and an **Attribute Value** to match against.</span></span> <span data-ttu-id="2a46c-147">The following operators are supported:</span><span class="sxs-lookup"><span data-stu-id="2a46c-147">The following operators are supported:</span></span>

   <span data-ttu-id="2a46c-148">a.</span><span class="sxs-lookup"><span data-stu-id="2a46c-148">a.</span></span> <span data-ttu-id="2a46c-149">**EQUALS**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-149">**EQUALS**.</span></span> <span data-ttu-id="2a46c-150">Clause returns "true" if the evaluated attribute matches the input string value exactly (case sensitive).</span><span class="sxs-lookup"><span data-stu-id="2a46c-150">Clause returns "true" if the evaluated attribute matches the input string value exactly (case sensitive).</span></span>

   <span data-ttu-id="2a46c-151">b.</span><span class="sxs-lookup"><span data-stu-id="2a46c-151">b.</span></span> <span data-ttu-id="2a46c-152">**NOT EQUALS**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-152">**NOT EQUALS**.</span></span> <span data-ttu-id="2a46c-153">Clause returns "true" if the evaluated attribute doesn't match the input string value (case sensitive).</span><span class="sxs-lookup"><span data-stu-id="2a46c-153">Clause returns "true" if the evaluated attribute doesn't match the input string value (case sensitive).</span></span>

   <span data-ttu-id="2a46c-154">c.</span><span class="sxs-lookup"><span data-stu-id="2a46c-154">c.</span></span> <span data-ttu-id="2a46c-155">**IS TRUE**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-155">**IS TRUE**.</span></span> <span data-ttu-id="2a46c-156">Clause returns "true" if the evaluated attribute contains a Boolean value of true.</span><span class="sxs-lookup"><span data-stu-id="2a46c-156">Clause returns "true" if the evaluated attribute contains a Boolean value of true.</span></span>

   <span data-ttu-id="2a46c-157">d.</span><span class="sxs-lookup"><span data-stu-id="2a46c-157">d.</span></span> <span data-ttu-id="2a46c-158">**IS FALSE**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-158">**IS FALSE**.</span></span> <span data-ttu-id="2a46c-159">Clause returns "true" if the evaluated attribute contains a Boolean value of false.</span><span class="sxs-lookup"><span data-stu-id="2a46c-159">Clause returns "true" if the evaluated attribute contains a Boolean value of false.</span></span>

   <span data-ttu-id="2a46c-160">e.</span><span class="sxs-lookup"><span data-stu-id="2a46c-160">e.</span></span> <span data-ttu-id="2a46c-161">**IS NULL**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-161">**IS NULL**.</span></span> <span data-ttu-id="2a46c-162">Clause returns "true" if the evaluated attribute is empty.</span><span class="sxs-lookup"><span data-stu-id="2a46c-162">Clause returns "true" if the evaluated attribute is empty.</span></span>

   <span data-ttu-id="2a46c-163">f.</span><span class="sxs-lookup"><span data-stu-id="2a46c-163">f.</span></span> <span data-ttu-id="2a46c-164">**IS NOT NULL**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-164">**IS NOT NULL**.</span></span> <span data-ttu-id="2a46c-165">Clause returns "true" if the evaluated attribute isn't empty.</span><span class="sxs-lookup"><span data-stu-id="2a46c-165">Clause returns "true" if the evaluated attribute isn't empty.</span></span>

   <span data-ttu-id="2a46c-166">g.</span><span class="sxs-lookup"><span data-stu-id="2a46c-166">g.</span></span> <span data-ttu-id="2a46c-167">**REGEX MATCH**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-167">**REGEX MATCH**.</span></span> <span data-ttu-id="2a46c-168">Clause returns "true" if the evaluated attribute matches a regular expression pattern.</span><span class="sxs-lookup"><span data-stu-id="2a46c-168">Clause returns "true" if the evaluated attribute matches a regular expression pattern.</span></span> <span data-ttu-id="2a46c-169">For example: ([1-9][0-9]) matches any number between 10 and 99.</span><span class="sxs-lookup"><span data-stu-id="2a46c-169">For example: ([1-9][0-9]) matches any number between 10 and 99.</span></span>

   <span data-ttu-id="2a46c-170">h.</span><span class="sxs-lookup"><span data-stu-id="2a46c-170">h.</span></span> <span data-ttu-id="2a46c-171">**NOT REGEX MATCH**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-171">**NOT REGEX MATCH**.</span></span> <span data-ttu-id="2a46c-172">Clause returns "true" if the evaluated attribute doesn't match a regular expression pattern.</span><span class="sxs-lookup"><span data-stu-id="2a46c-172">Clause returns "true" if the evaluated attribute doesn't match a regular expression pattern.</span></span>

8. <span data-ttu-id="2a46c-173">Select **Add new scoping clause**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-173">Select **Add new scoping clause**.</span></span>

9. <span data-ttu-id="2a46c-174">Optionally, repeat steps 7-8 to add more scoping clauses.</span><span class="sxs-lookup"><span data-stu-id="2a46c-174">Optionally, repeat steps 7-8 to add more scoping clauses.</span></span>

10. <span data-ttu-id="2a46c-175">In **Scoping Filter Title**, add a name for your scoping filter.</span><span class="sxs-lookup"><span data-stu-id="2a46c-175">In **Scoping Filter Title**, add a name for your scoping filter.</span></span>

11. <span data-ttu-id="2a46c-176">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="2a46c-176">Select **OK**.</span></span>

12. <span data-ttu-id="2a46c-177">Select **OK** again on the **Scoping Filters** screen.</span><span class="sxs-lookup"><span data-stu-id="2a46c-177">Select **OK** again on the **Scoping Filters** screen.</span></span> <span data-ttu-id="2a46c-178">Optionally, repeat steps 6-11 to add another scoping filter.</span><span class="sxs-lookup"><span data-stu-id="2a46c-178">Optionally, repeat steps 6-11 to add another scoping filter.</span></span>

13. <span data-ttu-id="2a46c-179">Select **Save** on the **Attribute Mapping** screen.</span><span class="sxs-lookup"><span data-stu-id="2a46c-179">Select **Save** on the **Attribute Mapping** screen.</span></span> 

>[!IMPORTANT] 
> <span data-ttu-id="2a46c-180">Saving a new scoping filter triggers a new full sync for the application, where all users in the source system are evaluated again against the new scoping filter.</span><span class="sxs-lookup"><span data-stu-id="2a46c-180">Saving a new scoping filter triggers a new full sync for the application, where all users in the source system are evaluated again against the new scoping filter.</span></span> <span data-ttu-id="2a46c-181">If a user in the application was previously in scope for provisioning, but falls out of scope, their account is disabled or deprovisioned in the application.</span><span class="sxs-lookup"><span data-stu-id="2a46c-181">If a user in the application was previously in scope for provisioning, but falls out of scope, their account is disabled or deprovisioned in the application.</span></span>


## <a name="related-articles"></a><span data-ttu-id="2a46c-182">Related articles</span><span class="sxs-lookup"><span data-stu-id="2a46c-182">Related articles</span></span>
* [<span data-ttu-id="2a46c-183">Article index for application management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2a46c-183">Article index for application management in Azure Active Directory</span></span>](../active-directory-apps-index.md)
* [<span data-ttu-id="2a46c-184">Automate user provisioning and deprovisioning to SaaS applications</span><span class="sxs-lookup"><span data-stu-id="2a46c-184">Automate user provisioning and deprovisioning to SaaS applications</span></span>](user-provisioning.md)
* [<span data-ttu-id="2a46c-185">Customize attribute mappings for user provisioning</span><span class="sxs-lookup"><span data-stu-id="2a46c-185">Customize attribute mappings for user provisioning</span></span>](customize-application-attributes.md)
* [<span data-ttu-id="2a46c-186">Write expressions for attribute mappings</span><span class="sxs-lookup"><span data-stu-id="2a46c-186">Write expressions for attribute mappings</span></span>](functions-for-customizing-application-data.md)
* [<span data-ttu-id="2a46c-187">Account provisioning notifications</span><span class="sxs-lookup"><span data-stu-id="2a46c-187">Account provisioning notifications</span></span>](user-provisioning.md)
* [<span data-ttu-id="2a46c-188">Use SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span><span class="sxs-lookup"><span data-stu-id="2a46c-188">Use SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](use-scim-to-provision-users-and-groups.md)
* [<span data-ttu-id="2a46c-189">List of tutorials on how to integrate SaaS apps</span><span class="sxs-lookup"><span data-stu-id="2a46c-189">List of tutorials on how to integrate SaaS apps</span></span>](../saas-apps/tutorial-list.md)

