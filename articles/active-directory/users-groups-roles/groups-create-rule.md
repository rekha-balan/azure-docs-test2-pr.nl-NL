---
title: Create a dynamic group and check status in Azure Active Directory | Microsoft Docs
description: How to create a group membership rules in the Azure portal, check status.
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 08/02/2018
ms.author: curtand
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 9a2eb8ab4e3ee65e97de578c825bf106aee1b829
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871303"
---
# <a name="create-a-dynamic-group-and-check-status"></a><span data-ttu-id="fe95c-103">Create a dynamic group and check status</span><span class="sxs-lookup"><span data-stu-id="fe95c-103">Create a dynamic group and check status</span></span>

<span data-ttu-id="fe95c-104">In Azure Active Directory (Azure AD), you can create groups by applying a rule to determine membership based on user or device properties.</span><span class="sxs-lookup"><span data-stu-id="fe95c-104">In Azure Active Directory (Azure AD), you can create groups by applying a rule to determine membership based on user or device properties.</span></span> <span data-ttu-id="fe95c-105">When the attributes of a user or device changes, Azure AD evaluates all dynamic group rules in the Azure AD tenant and performs any adds or removes.</span><span class="sxs-lookup"><span data-stu-id="fe95c-105">When the attributes of a user or device changes, Azure AD evaluates all dynamic group rules in the Azure AD tenant and performs any adds or removes.</span></span> <span data-ttu-id="fe95c-106">If a user or device satisfies a rule for a group, they are added as a member, and when they no longer satisfy the rule, they are removed.</span><span class="sxs-lookup"><span data-stu-id="fe95c-106">If a user or device satisfies a rule for a group, they are added as a member, and when they no longer satisfy the rule, they are removed.</span></span>

<span data-ttu-id="fe95c-107">This article details how to set up a rule in the Azure portal for dynamic membership on security groups or Office 365 groups.</span><span class="sxs-lookup"><span data-stu-id="fe95c-107">This article details how to set up a rule in the Azure portal for dynamic membership on security groups or Office 365 groups.</span></span> <span data-ttu-id="fe95c-108">For examples of rule syntax and a complete list of the supported properties, operators, and values for a membership rule, see [Dynamic membership rules for groups in Azure Active Directory](groups-dynamic-membership.md).</span><span class="sxs-lookup"><span data-stu-id="fe95c-108">For examples of rule syntax and a complete list of the supported properties, operators, and values for a membership rule, see [Dynamic membership rules for groups in Azure Active Directory](groups-dynamic-membership.md).</span></span>

## <a name="to-create-a-group-membership-rule"></a><span data-ttu-id="fe95c-109">To create a group membership rule</span><span class="sxs-lookup"><span data-stu-id="fe95c-109">To create a group membership rule</span></span>

1. <span data-ttu-id="fe95c-110">Sign in to the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator or a user account administrator.</span><span class="sxs-lookup"><span data-stu-id="fe95c-110">Sign in to the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator or a user account administrator.</span></span>
2. <span data-ttu-id="fe95c-111">Select **Groups**.</span><span class="sxs-lookup"><span data-stu-id="fe95c-111">Select **Groups**.</span></span>
3. <span data-ttu-id="fe95c-112">Select **All groups**, and select **New group**.</span><span class="sxs-lookup"><span data-stu-id="fe95c-112">Select **All groups**, and select **New group**.</span></span>

   ![Add new group](./media/groups-create-rule/new-group-creation.png)

4. <span data-ttu-id="fe95c-114">On the **Group** blade, enter a name and description for the new group.</span><span class="sxs-lookup"><span data-stu-id="fe95c-114">On the **Group** blade, enter a name and description for the new group.</span></span> <span data-ttu-id="fe95c-115">Select a **Membership type** of either **Dynamic User** or **Dynamic Device**, depending on whether you want to create a rule for users or devices, and then select **Add dynamic query**.</span><span class="sxs-lookup"><span data-stu-id="fe95c-115">Select a **Membership type** of either **Dynamic User** or **Dynamic Device**, depending on whether you want to create a rule for users or devices, and then select **Add dynamic query**.</span></span> <span data-ttu-id="fe95c-116">You can use the rule builder to build a simple rule, or write a membership rule yourself.</span><span class="sxs-lookup"><span data-stu-id="fe95c-116">You can use the rule builder to build a simple rule, or write a membership rule yourself.</span></span> <span data-ttu-id="fe95c-117">This article contains more information about available user and device attributes as well as examples of membership rules.</span><span class="sxs-lookup"><span data-stu-id="fe95c-117">This article contains more information about available user and device attributes as well as examples of membership rules.</span></span>

   ![Add dynamic membership rule](./media/groups-create-rule/add-dynamic-group-rule.png)

5. <span data-ttu-id="fe95c-119">After creating the rule, select **Add query** at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="fe95c-119">After creating the rule, select **Add query** at the bottom of the blade.</span></span>
6. <span data-ttu-id="fe95c-120">Select **Create** on the **Group** blade to create the group.</span><span class="sxs-lookup"><span data-stu-id="fe95c-120">Select **Create** on the **Group** blade to create the group.</span></span>

> [!TIP]
> <span data-ttu-id="fe95c-121">Group creation fails if the rule you entered was incorrectly formed or not valid.</span><span class="sxs-lookup"><span data-stu-id="fe95c-121">Group creation fails if the rule you entered was incorrectly formed or not valid.</span></span> <span data-ttu-id="fe95c-122">A notification is displayed in the upper-right hand corner of the portal, containing an explanation of why the rule could not be processed.</span><span class="sxs-lookup"><span data-stu-id="fe95c-122">A notification is displayed in the upper-right hand corner of the portal, containing an explanation of why the rule could not be processed.</span></span> <span data-ttu-id="fe95c-123">Read it carefully to understand how you need to adjust the rule to make it valid.</span><span class="sxs-lookup"><span data-stu-id="fe95c-123">Read it carefully to understand how you need to adjust the rule to make it valid.</span></span>

## <a name="check-processing-status-for-a-membership-rule"></a><span data-ttu-id="fe95c-124">Check processing status for a membership rule</span><span class="sxs-lookup"><span data-stu-id="fe95c-124">Check processing status for a membership rule</span></span>

<span data-ttu-id="fe95c-125">You can see the membership processing status and the last updated date on the **Overview** page for the group.</span><span class="sxs-lookup"><span data-stu-id="fe95c-125">You can see the membership processing status and the last updated date on the **Overview** page for the group.</span></span>
  
  ![dynamic group status display](./media/groups-create-rule/group-status.png)

<span data-ttu-id="fe95c-127">The following status messages can be shown for **Membership processing** status:</span><span class="sxs-lookup"><span data-stu-id="fe95c-127">The following status messages can be shown for **Membership processing** status:</span></span>

* <span data-ttu-id="fe95c-128">**Evaluating**:  The group change has been received and the updates are being evaluated.</span><span class="sxs-lookup"><span data-stu-id="fe95c-128">**Evaluating**:  The group change has been received and the updates are being evaluated.</span></span>
* <span data-ttu-id="fe95c-129">**Processing**: Updates are being processed.</span><span class="sxs-lookup"><span data-stu-id="fe95c-129">**Processing**: Updates are being processed.</span></span>
* <span data-ttu-id="fe95c-130">**Update complete**: Processing has completed and all applicable updates have been made.</span><span class="sxs-lookup"><span data-stu-id="fe95c-130">**Update complete**: Processing has completed and all applicable updates have been made.</span></span>
* <span data-ttu-id="fe95c-131">**Processing error**: An error was encountered while evaluating the membership rule and processing could not be completed.</span><span class="sxs-lookup"><span data-stu-id="fe95c-131">**Processing error**: An error was encountered while evaluating the membership rule and processing could not be completed.</span></span>
* <span data-ttu-id="fe95c-132">**Update paused**: Dynamic membership rule updates have been paused by the administrator.</span><span class="sxs-lookup"><span data-stu-id="fe95c-132">**Update paused**: Dynamic membership rule updates have been paused by the administrator.</span></span> <span data-ttu-id="fe95c-133">MembershipRuleProcessingState is set to “Paused”.</span><span class="sxs-lookup"><span data-stu-id="fe95c-133">MembershipRuleProcessingState is set to “Paused”.</span></span>

<span data-ttu-id="fe95c-134">The following status messages can be shown for **Membership last updated** status:</span><span class="sxs-lookup"><span data-stu-id="fe95c-134">The following status messages can be shown for **Membership last updated** status:</span></span>

* <span data-ttu-id="fe95c-135">&lt;**Date and time**&gt;: The last time the membership was updated.</span><span class="sxs-lookup"><span data-stu-id="fe95c-135">&lt;**Date and time**&gt;: The last time the membership was updated.</span></span>
* <span data-ttu-id="fe95c-136">**In Progress**: Updates are currently in progress.</span><span class="sxs-lookup"><span data-stu-id="fe95c-136">**In Progress**: Updates are currently in progress.</span></span>
* <span data-ttu-id="fe95c-137">**Unknown**: The last update time cannot be retrieved.</span><span class="sxs-lookup"><span data-stu-id="fe95c-137">**Unknown**: The last update time cannot be retrieved.</span></span> <span data-ttu-id="fe95c-138">It may be due to the group being newly created.</span><span class="sxs-lookup"><span data-stu-id="fe95c-138">It may be due to the group being newly created.</span></span>

<span data-ttu-id="fe95c-139">If an error occurs while processing the membership rule for a specific group, an alert is shown on the top of the **Overview page** for the group.</span><span class="sxs-lookup"><span data-stu-id="fe95c-139">If an error occurs while processing the membership rule for a specific group, an alert is shown on the top of the **Overview page** for the group.</span></span> <span data-ttu-id="fe95c-140">If no pending dynamic membership updates can be processed for all the groups within the tenant for more then 24 hours, an alert is shown on the top of **All groups**.</span><span class="sxs-lookup"><span data-stu-id="fe95c-140">If no pending dynamic membership updates can be processed for all the groups within the tenant for more then 24 hours, an alert is shown on the top of **All groups**.</span></span>

![processing error message](./media/groups-create-rule/processing-error.png)

<span data-ttu-id="fe95c-142">These articles provide additional information on groups in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fe95c-142">These articles provide additional information on groups in Azure Active Directory.</span></span>

* [<span data-ttu-id="fe95c-143">See existing groups</span><span class="sxs-lookup"><span data-stu-id="fe95c-143">See existing groups</span></span>](../fundamentals/active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="fe95c-144">Create a new group and adding members</span><span class="sxs-lookup"><span data-stu-id="fe95c-144">Create a new group and adding members</span></span>](../fundamentals/active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="fe95c-145">Manage settings of a group</span><span class="sxs-lookup"><span data-stu-id="fe95c-145">Manage settings of a group</span></span>](../fundamentals/active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="fe95c-146">Manage memberships of a group</span><span class="sxs-lookup"><span data-stu-id="fe95c-146">Manage memberships of a group</span></span>](../fundamentals/active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="fe95c-147">Manage dynamic rules for users in a group</span><span class="sxs-lookup"><span data-stu-id="fe95c-147">Manage dynamic rules for users in a group</span></span>](groups-dynamic-membership.md)
