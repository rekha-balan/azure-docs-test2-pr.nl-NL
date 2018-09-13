---
title: Change static group membership type to dynamic in Azure Active Directory | Microsoft Docs
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
ms.openlocfilehash: 4cc9c446c1a8ff7c82b08ba9787a40598a8b4cd4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856905"
---
# <a name="change-static-group-membership-to-dynamic-in-azure-active-directory"></a><span data-ttu-id="f0e71-103">Change static group membership to dynamic in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0e71-103">Change static group membership to dynamic in Azure Active Directory</span></span>

<span data-ttu-id="f0e71-104">You can change a group's membership from static to dynamic (or vice-versa) In Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0e71-104">You can change a group's membership from static to dynamic (or vice-versa) In Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f0e71-105">Azure AD keeps the same group name and ID in the system, so all existing references to the group are still valid.</span><span class="sxs-lookup"><span data-stu-id="f0e71-105">Azure AD keeps the same group name and ID in the system, so all existing references to the group are still valid.</span></span> <span data-ttu-id="f0e71-106">If you create a new group instead, you would need to update those references.</span><span class="sxs-lookup"><span data-stu-id="f0e71-106">If you create a new group instead, you would need to update those references.</span></span> <span data-ttu-id="f0e71-107">Dynamic group membership eliminates management overhead adding and removing users.</span><span class="sxs-lookup"><span data-stu-id="f0e71-107">Dynamic group membership eliminates management overhead adding and removing users.</span></span> <span data-ttu-id="f0e71-108">This article tells you how to convert existing groups from static to dynamic membership using either Azure AD Admin center or PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f0e71-108">This article tells you how to convert existing groups from static to dynamic membership using either Azure AD Admin center or PowerShell cmdlets.</span></span>

> [!WARNING]
> <span data-ttu-id="f0e71-109">When changing an existing static group to a dynamic group, all existing members are removed from the group, and then the membership rule is processed to add new members.</span><span class="sxs-lookup"><span data-stu-id="f0e71-109">When changing an existing static group to a dynamic group, all existing members are removed from the group, and then the membership rule is processed to add new members.</span></span> <span data-ttu-id="f0e71-110">If the group is used to control access to apps or resources, be aware that the original members might lose access until the membership rule is fully processed.</span><span class="sxs-lookup"><span data-stu-id="f0e71-110">If the group is used to control access to apps or resources, be aware that the original members might lose access until the membership rule is fully processed.</span></span>
>
> <span data-ttu-id="f0e71-111">We recommend that you test the new membership rule beforehand to make sure that the new membership in the group is as expected.</span><span class="sxs-lookup"><span data-stu-id="f0e71-111">We recommend that you test the new membership rule beforehand to make sure that the new membership in the group is as expected.</span></span>

## <a name="change-the-membership-type-for-a-group"></a><span data-ttu-id="f0e71-112">Change the membership type for a group</span><span class="sxs-lookup"><span data-stu-id="f0e71-112">Change the membership type for a group</span></span>

1. <span data-ttu-id="f0e71-113">Sign in to the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator or a user account administrator in your tenant.</span><span class="sxs-lookup"><span data-stu-id="f0e71-113">Sign in to the [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator or a user account administrator in your tenant.</span></span>
2. <span data-ttu-id="f0e71-114">Select **Groups**.</span><span class="sxs-lookup"><span data-stu-id="f0e71-114">Select **Groups**.</span></span>
3. <span data-ttu-id="f0e71-115">From the **All groups** list, open the group that you want to change.</span><span class="sxs-lookup"><span data-stu-id="f0e71-115">From the **All groups** list, open the group that you want to change.</span></span>
4. <span data-ttu-id="f0e71-116">Select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="f0e71-116">Select **Properties**.</span></span>
5. <span data-ttu-id="f0e71-117">On the **Properties** page for the group, select a **Membership type** of either Assigned (static), Dynamic User, or Dynamic Device, depending on your desired membership type.</span><span class="sxs-lookup"><span data-stu-id="f0e71-117">On the **Properties** page for the group, select a **Membership type** of either Assigned (static), Dynamic User, or Dynamic Device, depending on your desired membership type.</span></span> <span data-ttu-id="f0e71-118">For dynamic membership, you can use the rule builder to select options for a simple rule or write a membership rule yourself.</span><span class="sxs-lookup"><span data-stu-id="f0e71-118">For dynamic membership, you can use the rule builder to select options for a simple rule or write a membership rule yourself.</span></span> 

<span data-ttu-id="f0e71-119">The following steps are an example of changing a group from static to dynamic membership for a group of users.</span><span class="sxs-lookup"><span data-stu-id="f0e71-119">The following steps are an example of changing a group from static to dynamic membership for a group of users.</span></span>

1. <span data-ttu-id="f0e71-120">On the **Properties** page for your selected group, select a **Membership type** of **Dynamic User**, then select Yes on the dialog explaining the changes to the group membership to continue.</span><span class="sxs-lookup"><span data-stu-id="f0e71-120">On the **Properties** page for your selected group, select a **Membership type** of **Dynamic User**, then select Yes on the dialog explaining the changes to the group membership to continue.</span></span> 
  
   ![select membership type of dynamic user](./media/groups-change-type/select-group-to-convert.png)
  
2. <span data-ttu-id="f0e71-122">Select **Add dynamic query**, and then provide the rule.</span><span class="sxs-lookup"><span data-stu-id="f0e71-122">Select **Add dynamic query**, and then provide the rule.</span></span>
  
   ![enter the rule](./media/groups-change-type/enter-rule.png)
  
3. <span data-ttu-id="f0e71-124">After creating the rule, select **Add query** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="f0e71-124">After creating the rule, select **Add query** at the bottom of the page.</span></span>
4. <span data-ttu-id="f0e71-125">Select **Save** on the **Properties** page for the group to save your changes.</span><span class="sxs-lookup"><span data-stu-id="f0e71-125">Select **Save** on the **Properties** page for the group to save your changes.</span></span> <span data-ttu-id="f0e71-126">The **Membership type** of the group is immediately updated in the group list.</span><span class="sxs-lookup"><span data-stu-id="f0e71-126">The **Membership type** of the group is immediately updated in the group list.</span></span>

> [!TIP]
> <span data-ttu-id="f0e71-127">Group conversion might fail if the membership rule you entered was incorrect.</span><span class="sxs-lookup"><span data-stu-id="f0e71-127">Group conversion might fail if the membership rule you entered was incorrect.</span></span> <span data-ttu-id="f0e71-128">A notification is displayed in the upper-right hand corner of the portal that it contains an explanation of why the rule can't be accepted by the system.</span><span class="sxs-lookup"><span data-stu-id="f0e71-128">A notification is displayed in the upper-right hand corner of the portal that it contains an explanation of why the rule can't be accepted by the system.</span></span> <span data-ttu-id="f0e71-129">Read it carefully to understand how you can adjust the rule to make it valid.</span><span class="sxs-lookup"><span data-stu-id="f0e71-129">Read it carefully to understand how you can adjust the rule to make it valid.</span></span> <span data-ttu-id="f0e71-130">For examples of rule syntax and a complete list of the supported properties, operators, and values for a membership rule, see [Dynamic membership rules for groups in Azure Active Directory](groups-dynamic-membership.md).</span><span class="sxs-lookup"><span data-stu-id="f0e71-130">For examples of rule syntax and a complete list of the supported properties, operators, and values for a membership rule, see [Dynamic membership rules for groups in Azure Active Directory](groups-dynamic-membership.md).</span></span>


## <a name="change-membership-type-for-a-group-powershell"></a><span data-ttu-id="f0e71-131">Change membership type for a group (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="f0e71-131">Change membership type for a group (PowerShell)</span></span>

> [!NOTE]
> <span data-ttu-id="f0e71-132">To change dynamic group properties you will need to use cmdlets from **the preview version of** [Azure AD PowerShell Version 2](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="f0e71-132">To change dynamic group properties you will need to use cmdlets from **the preview version of** [Azure AD PowerShell Version 2](https://docs.microsoft.com/powershell/azure/active-directory/install-adv2?view=azureadps-2.0).</span></span> <span data-ttu-id="f0e71-133">You can install the preview from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="f0e71-133">You can install the preview from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

<span data-ttu-id="f0e71-134">Here is an example of functions that switch membership management on an existing group.</span><span class="sxs-lookup"><span data-stu-id="f0e71-134">Here is an example of functions that switch membership management on an existing group.</span></span> <span data-ttu-id="f0e71-135">In this example, care is taken to correctly manipulate the GroupTypes property and preserve any values that are unrelated to dynamic membership.</span><span class="sxs-lookup"><span data-stu-id="f0e71-135">In this example, care is taken to correctly manipulate the GroupTypes property and preserve any values that are unrelated to dynamic membership.</span></span>

```
#The moniker for dynamic groups as used in the GroupTypes property of a group object
$dynamicGroupTypeString = "DynamicMembership"

function ConvertDynamicGroupToStatic
{
    Param([string]$groupId)

    #existing group types
    [System.Collections.ArrayList]$groupTypes = (Get-AzureAdMsGroup -Id $groupId).GroupTypes

    if($groupTypes -eq $null -or !$groupTypes.Contains($dynamicGroupTypeString))
    {
        throw "This group is already a static group. Aborting conversion.";
    }


    #remove the type for dynamic groups, but keep the other type values
    $groupTypes.Remove($dynamicGroupTypeString)

    #modify the group properties to make it a static group: i) change GroupTypes to remove the dynamic type, ii) pause execution of the current rule
    Set-AzureAdMsGroup -Id $groupId -GroupTypes $groupTypes.ToArray() -MembershipRuleProcessingState "Paused"
}

function ConvertStaticGroupToDynamic
{
    Param([string]$groupId, [string]$dynamicMembershipRule)

    #existing group types
    [System.Collections.ArrayList]$groupTypes = (Get-AzureAdMsGroup -Id $groupId).GroupTypes

    if($groupTypes -ne $null -and $groupTypes.Contains($dynamicGroupTypeString))
    {
        throw "This group is already a dynamic group. Aborting conversion.";
    }
    #add the dynamic group type to existing types
    $groupTypes.Add($dynamicGroupTypeString)

    #modify the group properties to make it a static group: i) change GroupTypes to add the dynamic type, ii) start execution of the rule, iii) set the rule
    Set-AzureAdMsGroup -Id $groupId -GroupTypes $groupTypes.ToArray() -MembershipRuleProcessingState "On" -MembershipRule $dynamicMembershipRule
}
```
<span data-ttu-id="f0e71-136">To make a group static:</span><span class="sxs-lookup"><span data-stu-id="f0e71-136">To make a group static:</span></span>

```
ConvertDynamicGroupToStatic "a58913b2-eee4-44f9-beb2-e381c375058f"
```

<span data-ttu-id="f0e71-137">To make a group dynamic:</span><span class="sxs-lookup"><span data-stu-id="f0e71-137">To make a group dynamic:</span></span>

```
ConvertStaticGroupToDynamic "a58913b2-eee4-44f9-beb2-e381c375058f" "user.displayName -startsWith ""Peter"""
```

## <a name="next-steps"></a><span data-ttu-id="f0e71-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="f0e71-138">Next steps</span></span>

<span data-ttu-id="f0e71-139">These articles provide additional information on groups in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f0e71-139">These articles provide additional information on groups in Azure Active Directory.</span></span>

* [<span data-ttu-id="f0e71-140">See existing groups</span><span class="sxs-lookup"><span data-stu-id="f0e71-140">See existing groups</span></span>](../fundamentals/active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="f0e71-141">Create a new group and adding members</span><span class="sxs-lookup"><span data-stu-id="f0e71-141">Create a new group and adding members</span></span>](../fundamentals/active-directory-groups-create-azure-portal.md)
* [<span data-ttu-id="f0e71-142">Manage settings of a group</span><span class="sxs-lookup"><span data-stu-id="f0e71-142">Manage settings of a group</span></span>](../fundamentals/active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="f0e71-143">Manage memberships of a group</span><span class="sxs-lookup"><span data-stu-id="f0e71-143">Manage memberships of a group</span></span>](../fundamentals/active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="f0e71-144">Manage dynamic rules for users in a group</span><span class="sxs-lookup"><span data-stu-id="f0e71-144">Manage dynamic rules for users in a group</span></span>](groups-dynamic-membership.md)
