---
title: Managing groups in Azure Active Directory | Microsoft Docs
description: How to create and manage groups to manage Azure users using Azure Active Directory.
services: active-directory
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/10/2017
ms.author: curtand
ms.openlocfilehash: 7d2cc99925e01f8135f04f5863f798e13d7413e3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555874"
---
# <a name="managing-groups-in-azure-active-directory"></a><span data-ttu-id="e27c0-103">Managing groups in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e27c0-103">Managing groups in Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](active-directory-groups-create-azure-portal.md)
> * [Azure classic portal](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="e27c0-107">One of the features of Azure Active Directory (Azure AD) user management is the ability to create groups of users.</span><span class="sxs-lookup"><span data-stu-id="e27c0-107">One of the features of Azure Active Directory (Azure AD) user management is the ability to create groups of users.</span></span> <span data-ttu-id="e27c0-108">You use a group to perform management tasks such as assigning licenses or permissions to a number of users at once.</span><span class="sxs-lookup"><span data-stu-id="e27c0-108">You use a group to perform management tasks such as assigning licenses or permissions to a number of users at once.</span></span> <span data-ttu-id="e27c0-109">You can also use groups to assign access permission to</span><span class="sxs-lookup"><span data-stu-id="e27c0-109">You can also use groups to assign access permission to</span></span>

* <span data-ttu-id="e27c0-110">Resources such as objects in the directory</span><span class="sxs-lookup"><span data-stu-id="e27c0-110">Resources such as objects in the directory</span></span>
* <span data-ttu-id="e27c0-111">Resources external to the directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span><span class="sxs-lookup"><span data-stu-id="e27c0-111">Resources external to the directory such as SaaS applications, Azure services, SharePoint sites, or on-premises resources</span></span>

<span data-ttu-id="e27c0-112">In addition, a resource owner can also assign access to a resource to an Azure AD group owned by someone else.</span><span class="sxs-lookup"><span data-stu-id="e27c0-112">In addition, a resource owner can also assign access to a resource to an Azure AD group owned by someone else.</span></span> <span data-ttu-id="e27c0-113">This assignment grants the members of that group access to the resource.</span><span class="sxs-lookup"><span data-stu-id="e27c0-113">This assignment grants the members of that group access to the resource.</span></span> <span data-ttu-id="e27c0-114">Then, the owner of the group manages membership in the group.</span><span class="sxs-lookup"><span data-stu-id="e27c0-114">Then, the owner of the group manages membership in the group.</span></span> <span data-ttu-id="e27c0-115">Effectively, the resource owner delegates to the owner of the group the permission to assign users to their resource.</span><span class="sxs-lookup"><span data-stu-id="e27c0-115">Effectively, the resource owner delegates to the owner of the group the permission to assign users to their resource.</span></span>

## <a name="how-do-i-create-a-group"></a><span data-ttu-id="e27c0-116">How do I create a group?</span><span class="sxs-lookup"><span data-stu-id="e27c0-116">How do I create a group?</span></span>
<span data-ttu-id="e27c0-117">Depending on the services to which your organization has subscribed, you can create a group using one of the following:</span><span class="sxs-lookup"><span data-stu-id="e27c0-117">Depending on the services to which your organization has subscribed, you can create a group using one of the following:</span></span>

* <span data-ttu-id="e27c0-118">the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="e27c0-118">the Azure classic portal</span></span>
* <span data-ttu-id="e27c0-119">the Office 365 account portal</span><span class="sxs-lookup"><span data-stu-id="e27c0-119">the Office 365 account portal</span></span>
* <span data-ttu-id="e27c0-120">the Windows Intune account portal</span><span class="sxs-lookup"><span data-stu-id="e27c0-120">the Windows Intune account portal</span></span>

<span data-ttu-id="e27c0-121">We'll describe tasks as performed in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="e27c0-121">We'll describe tasks as performed in the Azure classic portal.</span></span> <span data-ttu-id="e27c0-122">For more information about using non-Azure portals to manage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span><span class="sxs-lookup"><span data-stu-id="e27c0-122">For more information about using non-Azure portals to manage your Azure AD directory, see [Administering your Azure AD directory](active-directory-administer.md).</span></span>

1. <span data-ttu-id="e27c0-123">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span><span class="sxs-lookup"><span data-stu-id="e27c0-123">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="e27c0-124">Select the **Groups** tab.</span><span class="sxs-lookup"><span data-stu-id="e27c0-124">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="e27c0-125">Select **Add Group**.</span><span class="sxs-lookup"><span data-stu-id="e27c0-125">Select **Add Group**.</span></span>
4. <span data-ttu-id="e27c0-126">In the **Add Group** window, specify the name and the description of a group.</span><span class="sxs-lookup"><span data-stu-id="e27c0-126">In the **Add Group** window, specify the name and the description of a group.</span></span>

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a><span data-ttu-id="e27c0-127">How do I add or remove individual users in a security group?</span><span class="sxs-lookup"><span data-stu-id="e27c0-127">How do I add or remove individual users in a security group?</span></span>
<span data-ttu-id="e27c0-128">**To add an individual user to a group**</span><span class="sxs-lookup"><span data-stu-id="e27c0-128">**To add an individual user to a group**</span></span>

1. <span data-ttu-id="e27c0-129">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span><span class="sxs-lookup"><span data-stu-id="e27c0-129">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="e27c0-130">Select the **Groups** tab.</span><span class="sxs-lookup"><span data-stu-id="e27c0-130">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="e27c0-131">Open the group to which you want to add members.</span><span class="sxs-lookup"><span data-stu-id="e27c0-131">Open the group to which you want to add members.</span></span> <span data-ttu-id="e27c0-132">Open the **Members** tab of the selected group if it not already displaying.</span><span class="sxs-lookup"><span data-stu-id="e27c0-132">Open the **Members** tab of the selected group if it not already displaying.</span></span>
4. <span data-ttu-id="e27c0-133">Select **Add Members**.</span><span class="sxs-lookup"><span data-stu-id="e27c0-133">Select **Add Members**.</span></span>
5. <span data-ttu-id="e27c0-134">On the **Add Members** page, select the name of the user or a group that you want to add as a member of this group.</span><span class="sxs-lookup"><span data-stu-id="e27c0-134">On the **Add Members** page, select the name of the user or a group that you want to add as a member of this group.</span></span> <span data-ttu-id="e27c0-135">Make sure that this name is added to the **Selected** pane.</span><span class="sxs-lookup"><span data-stu-id="e27c0-135">Make sure that this name is added to the **Selected** pane.</span></span>

<span data-ttu-id="e27c0-136">**To remove an individual user from a group**</span><span class="sxs-lookup"><span data-stu-id="e27c0-136">**To remove an individual user from a group**</span></span>

1. <span data-ttu-id="e27c0-137">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span><span class="sxs-lookup"><span data-stu-id="e27c0-137">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="e27c0-138">Select the **Groups** tab.</span><span class="sxs-lookup"><span data-stu-id="e27c0-138">Select the **Groups** tab.</span></span>
3. <span data-ttu-id="e27c0-139">Open the group from which you want to remove members.</span><span class="sxs-lookup"><span data-stu-id="e27c0-139">Open the group from which you want to remove members.</span></span>
4. <span data-ttu-id="e27c0-140">Select the **Members** tab, select the name of the member that you want to remove from this group, and then click **Remove**.</span><span class="sxs-lookup"><span data-stu-id="e27c0-140">Select the **Members** tab, select the name of the member that you want to remove from this group, and then click **Remove**.</span></span>
5. <span data-ttu-id="e27c0-141">Confirm at the prompt that you want to remove this member from the group.</span><span class="sxs-lookup"><span data-stu-id="e27c0-141">Confirm at the prompt that you want to remove this member from the group.</span></span>

## <a name="how-can-i-manage-the-membership-of-a-group-dynamically"></a><span data-ttu-id="e27c0-142">How can I manage the membership of a group dynamically?</span><span class="sxs-lookup"><span data-stu-id="e27c0-142">How can I manage the membership of a group dynamically?</span></span>
<span data-ttu-id="e27c0-143">In Azure AD, you can very easily set up a simple rule to determine which users are to be members of the group.</span><span class="sxs-lookup"><span data-stu-id="e27c0-143">In Azure AD, you can very easily set up a simple rule to determine which users are to be members of the group.</span></span> <span data-ttu-id="e27c0-144">A simple rule is one that makes only a single comparison.</span><span class="sxs-lookup"><span data-stu-id="e27c0-144">A simple rule is one that makes only a single comparison.</span></span> <span data-ttu-id="e27c0-145">For example, if a group is assigned to a SaaS application, you can set up a rule to add users who have a job title of "Sales Rep."</span><span class="sxs-lookup"><span data-stu-id="e27c0-145">For example, if a group is assigned to a SaaS application, you can set up a rule to add users who have a job title of "Sales Rep."</span></span> <span data-ttu-id="e27c0-146">This rule then grants access to this SaaS application to all users with that job title in your directory.</span><span class="sxs-lookup"><span data-stu-id="e27c0-146">This rule then grants access to this SaaS application to all users with that job title in your directory.</span></span>

<span data-ttu-id="e27c0-147">When any attributes of a user change, the system evaluates all dynamic group rules in a directory to see if the attribute change of the user would trigger any group adds or removes.</span><span class="sxs-lookup"><span data-stu-id="e27c0-147">When any attributes of a user change, the system evaluates all dynamic group rules in a directory to see if the attribute change of the user would trigger any group adds or removes.</span></span> <span data-ttu-id="e27c0-148">If a user satisfies a rule on a group, they are added as a member to that group.</span><span class="sxs-lookup"><span data-stu-id="e27c0-148">If a user satisfies a rule on a group, they are added as a member to that group.</span></span> <span data-ttu-id="e27c0-149">If they no longer satisfy the rule of a group they are a member of, they are removed as a members from that group.</span><span class="sxs-lookup"><span data-stu-id="e27c0-149">If they no longer satisfy the rule of a group they are a member of, they are removed as a members from that group.</span></span>

> [!NOTE]
> You can set up a rule for dynamic membership on security groups or Office 365 groups. Nested group memberships aren't currently supported for group-based assignment to applications.
>
> Dynamic memberships for groups require an Azure AD Premium license to be assigned to
>
> * The administrator who manages the rule on a group
> * All members of the group
>
>

<span data-ttu-id="e27c0-155">**To enable dynamic membership for a group**</span><span class="sxs-lookup"><span data-stu-id="e27c0-155">**To enable dynamic membership for a group**</span></span>

1. <span data-ttu-id="e27c0-156">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span><span class="sxs-lookup"><span data-stu-id="e27c0-156">In the [Azure classic portal](https://manage.windowsazure.com), select **Active Directory**, and then select the name of the directory for your organization.</span></span>
2. <span data-ttu-id="e27c0-157">Select the **Groups** tab, and open the group you want to edit.</span><span class="sxs-lookup"><span data-stu-id="e27c0-157">Select the **Groups** tab, and open the group you want to edit.</span></span>
3. <span data-ttu-id="e27c0-158">Select the **Configure** tab, and then set **Enable Dynamic Memberships** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="e27c0-158">Select the **Configure** tab, and then set **Enable Dynamic Memberships** to **Yes**.</span></span>
4. <span data-ttu-id="e27c0-159">Set up a simple single rule for the group to control how dynamic membership for this group functions.</span><span class="sxs-lookup"><span data-stu-id="e27c0-159">Set up a simple single rule for the group to control how dynamic membership for this group functions.</span></span> <span data-ttu-id="e27c0-160">Make sure the **Add users where** option is selected, and then select a user property from the list (for example, department, jobTitle, etc.),</span><span class="sxs-lookup"><span data-stu-id="e27c0-160">Make sure the **Add users where** option is selected, and then select a user property from the list (for example, department, jobTitle, etc.),</span></span>
5. <span data-ttu-id="e27c0-161">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span><span class="sxs-lookup"><span data-stu-id="e27c0-161">Next, select a condition (Not Equals, Equals, Not Starts With, Starts With, Not Contains, Contains, Not Match, Match).</span></span>
6. <span data-ttu-id="e27c0-162">Specify a comparison value for the selected user property.</span><span class="sxs-lookup"><span data-stu-id="e27c0-162">Specify a comparison value for the selected user property.</span></span>

<span data-ttu-id="e27c0-163">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span><span class="sxs-lookup"><span data-stu-id="e27c0-163">To learn about how to create *advanced* rules (rules that can contain multiple comparisons) for dynamic group membership, see [Using attributes to create advanced rules](active-directory-accessmanagement-groups-with-advanced-rules.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="e27c0-164">Additional information</span><span class="sxs-lookup"><span data-stu-id="e27c0-164">Additional information</span></span>
<span data-ttu-id="e27c0-165">These articles provide additional information on Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e27c0-165">These articles provide additional information on Azure Active Directory.</span></span>

* [<span data-ttu-id="e27c0-166">Managing access to resources with Azure Active Directory groups</span><span class="sxs-lookup"><span data-stu-id="e27c0-166">Managing access to resources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="e27c0-167">Azure Active Directory cmdlets for configuring group settings</span><span class="sxs-lookup"><span data-stu-id="e27c0-167">Azure Active Directory cmdlets for configuring group settings</span></span>](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [<span data-ttu-id="e27c0-168">Article Index for Application Management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e27c0-168">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="e27c0-169">What is Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e27c0-169">What is Azure Active Directory?</span></span>](active-directory-whatis.md)
* [<span data-ttu-id="e27c0-170">Integrating your on-premises identities with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e27c0-170">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
