---
title: Provisioning apps with scoping filters | Microsoft Docs
description: Learn how to use scoping filters to prevent objects in apps that support automated user provisioning from actually being provisioned if an object doesn’t satisfy your business requirements.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: deee0f50a13c746af0b3020e6efbbf960178aa8e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549650"
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a><span data-ttu-id="473f1-103">Attribute-based application provisioning with scoping filters</span><span class="sxs-lookup"><span data-stu-id="473f1-103">Attribute-based application provisioning with scoping filters</span></span>
<span data-ttu-id="473f1-104">The objective of this section is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to the application.</span><span class="sxs-lookup"><span data-stu-id="473f1-104">The objective of this section is to explain how to use scoping filters to define attribute-based rules that determine which users are provisioned to the application.</span></span>

## <a name="clauses-and-scope-groups"></a><span data-ttu-id="473f1-105">Clauses and Scope Groups</span><span class="sxs-lookup"><span data-stu-id="473f1-105">Clauses and Scope Groups</span></span>
![Scoping Filter][1] 

<span data-ttu-id="473f1-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span><span class="sxs-lookup"><span data-stu-id="473f1-107">Scoping filters are defined by one or more **scope groups**, each of which hold one or more **clauses**.</span></span> <span data-ttu-id="473f1-108">To see the clauses for a particular scope group, expand it by clicking the arrow to the left of the group name.</span><span class="sxs-lookup"><span data-stu-id="473f1-108">To see the clauses for a particular scope group, expand it by clicking the arrow to the left of the group name.</span></span>

<span data-ttu-id="473f1-109">A **clause** determines which users are allowed to pass through the scoping filter by evaluating each user’s attributes.</span><span class="sxs-lookup"><span data-stu-id="473f1-109">A **clause** determines which users are allowed to pass through the scoping filter by evaluating each user’s attributes.</span></span> <span data-ttu-id="473f1-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into the application.</span><span class="sxs-lookup"><span data-stu-id="473f1-110">For example, you might have one clause that requires that a user’s ‘state’ attribute equal New York, so only New York users are provisioned into the application.</span></span>

![Scoping Group Name][2] 

<span data-ttu-id="473f1-112">Each **scope group** starts with one mandatory **clause**, as shown in the screenshot above.</span><span class="sxs-lookup"><span data-stu-id="473f1-112">Each **scope group** starts with one mandatory **clause**, as shown in the screenshot above.</span></span> <span data-ttu-id="473f1-113">This clause simply states that the user must first be assigned to the application before it’s evaluated by your scoping filters.</span><span class="sxs-lookup"><span data-stu-id="473f1-113">This clause simply states that the user must first be assigned to the application before it’s evaluated by your scoping filters.</span></span> <span data-ttu-id="473f1-114">This clause cannot be deleted or modified.</span><span class="sxs-lookup"><span data-stu-id="473f1-114">This clause cannot be deleted or modified.</span></span>

<span data-ttu-id="473f1-115">You can add new clauses or new scope groups by pressing the appropriate button.</span><span class="sxs-lookup"><span data-stu-id="473f1-115">You can add new clauses or new scope groups by pressing the appropriate button.</span></span> <span data-ttu-id="473f1-116">You can give each scope group a name by editing its **Scope Group Name** property.</span><span class="sxs-lookup"><span data-stu-id="473f1-116">You can give each scope group a name by editing its **Scope Group Name** property.</span></span>

## <a name="how-scoping-filters-are-evaluated"></a><span data-ttu-id="473f1-117">How Scoping Filters are Evaluated</span><span class="sxs-lookup"><span data-stu-id="473f1-117">How Scoping Filters are Evaluated</span></span>
<span data-ttu-id="473f1-118">During provisioning, we test every assigned user against your scoping filters to determine if that user deserves access to the application.</span><span class="sxs-lookup"><span data-stu-id="473f1-118">During provisioning, we test every assigned user against your scoping filters to determine if that user deserves access to the application.</span></span> <span data-ttu-id="473f1-119">You can think of each clause as being a test that must be passed in order for the user to avoid getting filtered out.</span><span class="sxs-lookup"><span data-stu-id="473f1-119">You can think of each clause as being a test that must be passed in order for the user to avoid getting filtered out.</span></span> 

<span data-ttu-id="473f1-120">If you have multiple scope groups defined, each user must pass at least one of them to access the application.</span><span class="sxs-lookup"><span data-stu-id="473f1-120">If you have multiple scope groups defined, each user must pass at least one of them to access the application.</span></span> <span data-ttu-id="473f1-121">Within each scope group, however, the user must pass every clause to pass that specific scope group.</span><span class="sxs-lookup"><span data-stu-id="473f1-121">Within each scope group, however, the user must pass every clause to pass that specific scope group.</span></span> 

<span data-ttu-id="473f1-122">In other words, you can think of scope groups as being OR’d together, and you can think of the clauses within them as being AND’d together.</span><span class="sxs-lookup"><span data-stu-id="473f1-122">In other words, you can think of scope groups as being OR’d together, and you can think of the clauses within them as being AND’d together.</span></span> <span data-ttu-id="473f1-123">For example, consider the scoping filter below:</span><span class="sxs-lookup"><span data-stu-id="473f1-123">For example, consider the scoping filter below:</span></span>

![Scoping Group Name][3]  

<span data-ttu-id="473f1-125">According to this scoping filter, users must satisfy the following criteria, to be provisioned:</span><span class="sxs-lookup"><span data-stu-id="473f1-125">According to this scoping filter, users must satisfy the following criteria, to be provisioned:</span></span>

1. <span data-ttu-id="473f1-126">They must be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="473f1-126">They must be assigned to the application.</span></span>
2. <span data-ttu-id="473f1-127">They must work in the Engineering department</span><span class="sxs-lookup"><span data-stu-id="473f1-127">They must work in the Engineering department</span></span>
3. <span data-ttu-id="473f1-128">They must be work in either San Francisco or Canada.</span><span class="sxs-lookup"><span data-stu-id="473f1-128">They must be work in either San Francisco or Canada.</span></span>

## <a name="related-articles"></a><span data-ttu-id="473f1-129">Related Articles</span><span class="sxs-lookup"><span data-stu-id="473f1-129">Related Articles</span></span>
* [<span data-ttu-id="473f1-130">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="473f1-130">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="473f1-131">Automate User Provisioning and Deprovisioning to SaaS Applications</span><span class="sxs-lookup"><span data-stu-id="473f1-131">Automate User Provisioning and Deprovisioning to SaaS Applications</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="473f1-132">Customizing Attribute Mappings for User Provisioning</span><span class="sxs-lookup"><span data-stu-id="473f1-132">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="473f1-133">Writing Expressions for Attribute Mappings</span><span class="sxs-lookup"><span data-stu-id="473f1-133">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="473f1-134">Account Provisioning Notifications</span><span class="sxs-lookup"><span data-stu-id="473f1-134">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="473f1-135">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span><span class="sxs-lookup"><span data-stu-id="473f1-135">Using SCIM to enable automatic provisioning of users and groups from Azure Active Directory to applications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="473f1-136">List of Tutorials on How to Integrate SaaS Apps</span><span class="sxs-lookup"><span data-stu-id="473f1-136">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scoping-filters/ic782811.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scoping-filters/ic782812.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-saas-scoping-filters/ic782813.png



