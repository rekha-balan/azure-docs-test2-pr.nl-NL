---
title: Add owners and users in Azure DevTest Labs| Microsoft Docs
description: Add owners and users in Azure DevTest Labs using either the Azure portal or PowerShell
services: devtest-lab,virtual-machines
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.assetid: 4f51d9a5-2702-45f0-a2d5-a3635b58c416
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2018
ms.author: spelluru
ms.openlocfilehash: 8f9504458b1f332193e8457bcc9cf41e85fd6aca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870562"
---
# <a name="add-owners-and-users-in-azure-devtest-labs"></a><span data-ttu-id="adfbe-103">Add owners and users in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="adfbe-103">Add owners and users in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-security-in-your-DevTest-Lab/player]
> 
> 

<span data-ttu-id="adfbe-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../role-based-access-control/overview.md).</span><span class="sxs-lookup"><span data-stu-id="adfbe-104">Access in Azure DevTest Labs is controlled by [Azure Role-Based Access Control (RBAC)](../role-based-access-control/overview.md).</span></span> <span data-ttu-id="adfbe-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only the amount of access necessary to users to perform their jobs.</span><span class="sxs-lookup"><span data-stu-id="adfbe-105">Using RBAC, you can segregate duties within your team into *roles* where you grant only the amount of access necessary to users to perform their jobs.</span></span> <span data-ttu-id="adfbe-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span><span class="sxs-lookup"><span data-stu-id="adfbe-106">Three of these RBAC roles are *Owner*, *DevTest Labs User*, and *Contributor*.</span></span> <span data-ttu-id="adfbe-107">In this article, you learn what actions can be performed in each of the three main RBAC roles.</span><span class="sxs-lookup"><span data-stu-id="adfbe-107">In this article, you learn what actions can be performed in each of the three main RBAC roles.</span></span> <span data-ttu-id="adfbe-108">From there, you learn how to add users to a lab - both via the portal and via a PowerShell script, and how to add users at the subscription level.</span><span class="sxs-lookup"><span data-stu-id="adfbe-108">From there, you learn how to add users to a lab - both via the portal and via a PowerShell script, and how to add users at the subscription level.</span></span>

## <a name="actions-that-can-be-performed-in-each-role"></a><span data-ttu-id="adfbe-109">Actions that can be performed in each role</span><span class="sxs-lookup"><span data-stu-id="adfbe-109">Actions that can be performed in each role</span></span>
<span data-ttu-id="adfbe-110">There are three main roles that you can assign a user:</span><span class="sxs-lookup"><span data-stu-id="adfbe-110">There are three main roles that you can assign a user:</span></span>

* <span data-ttu-id="adfbe-111">Owner</span><span class="sxs-lookup"><span data-stu-id="adfbe-111">Owner</span></span>
* <span data-ttu-id="adfbe-112">DevTest Labs User</span><span class="sxs-lookup"><span data-stu-id="adfbe-112">DevTest Labs User</span></span>
* <span data-ttu-id="adfbe-113">Contributor</span><span class="sxs-lookup"><span data-stu-id="adfbe-113">Contributor</span></span>

<span data-ttu-id="adfbe-114">The following table illustrates the actions that can be performed by users in each of these roles:</span><span class="sxs-lookup"><span data-stu-id="adfbe-114">The following table illustrates the actions that can be performed by users in each of these roles:</span></span>

| <span data-ttu-id="adfbe-115">**Actions users in this role can perform**</span><span class="sxs-lookup"><span data-stu-id="adfbe-115">**Actions users in this role can perform**</span></span> | <span data-ttu-id="adfbe-116">**DevTest Labs User**</span><span class="sxs-lookup"><span data-stu-id="adfbe-116">**DevTest Labs User**</span></span> | <span data-ttu-id="adfbe-117">**Owner**</span><span class="sxs-lookup"><span data-stu-id="adfbe-117">**Owner**</span></span> | <span data-ttu-id="adfbe-118">**Contributor**</span><span class="sxs-lookup"><span data-stu-id="adfbe-118">**Contributor**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="adfbe-119">**Lab tasks**</span><span class="sxs-lookup"><span data-stu-id="adfbe-119">**Lab tasks**</span></span> | | | |
| <span data-ttu-id="adfbe-120">Add users to a lab</span><span class="sxs-lookup"><span data-stu-id="adfbe-120">Add users to a lab</span></span> |<span data-ttu-id="adfbe-121">No</span><span class="sxs-lookup"><span data-stu-id="adfbe-121">No</span></span> |<span data-ttu-id="adfbe-122">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-122">Yes</span></span> |<span data-ttu-id="adfbe-123">No</span><span class="sxs-lookup"><span data-stu-id="adfbe-123">No</span></span> |
| <span data-ttu-id="adfbe-124">Update cost settings</span><span class="sxs-lookup"><span data-stu-id="adfbe-124">Update cost settings</span></span> |<span data-ttu-id="adfbe-125">No</span><span class="sxs-lookup"><span data-stu-id="adfbe-125">No</span></span> |<span data-ttu-id="adfbe-126">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-126">Yes</span></span> |<span data-ttu-id="adfbe-127">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-127">Yes</span></span> |
| <span data-ttu-id="adfbe-128">**VM base tasks**</span><span class="sxs-lookup"><span data-stu-id="adfbe-128">**VM base tasks**</span></span> | | | |
| <span data-ttu-id="adfbe-129">Add and remove custom images</span><span class="sxs-lookup"><span data-stu-id="adfbe-129">Add and remove custom images</span></span> |<span data-ttu-id="adfbe-130">No</span><span class="sxs-lookup"><span data-stu-id="adfbe-130">No</span></span> |<span data-ttu-id="adfbe-131">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-131">Yes</span></span> |<span data-ttu-id="adfbe-132">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-132">Yes</span></span> |
| <span data-ttu-id="adfbe-133">Add, update, and delete formulas</span><span class="sxs-lookup"><span data-stu-id="adfbe-133">Add, update, and delete formulas</span></span> |<span data-ttu-id="adfbe-134">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-134">Yes</span></span> |<span data-ttu-id="adfbe-135">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-135">Yes</span></span> |<span data-ttu-id="adfbe-136">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-136">Yes</span></span> |
| <span data-ttu-id="adfbe-137">Whitelist Azure Marketplace images</span><span class="sxs-lookup"><span data-stu-id="adfbe-137">Whitelist Azure Marketplace images</span></span> |<span data-ttu-id="adfbe-138">No</span><span class="sxs-lookup"><span data-stu-id="adfbe-138">No</span></span> |<span data-ttu-id="adfbe-139">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-139">Yes</span></span> |<span data-ttu-id="adfbe-140">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-140">Yes</span></span> |
| <span data-ttu-id="adfbe-141">**VM tasks**</span><span class="sxs-lookup"><span data-stu-id="adfbe-141">**VM tasks**</span></span> | | | |
| <span data-ttu-id="adfbe-142">Create VMs</span><span class="sxs-lookup"><span data-stu-id="adfbe-142">Create VMs</span></span> |<span data-ttu-id="adfbe-143">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-143">Yes</span></span> |<span data-ttu-id="adfbe-144">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-144">Yes</span></span> |<span data-ttu-id="adfbe-145">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-145">Yes</span></span> |
| <span data-ttu-id="adfbe-146">Start, stop, and delete VMs</span><span class="sxs-lookup"><span data-stu-id="adfbe-146">Start, stop, and delete VMs</span></span> |<span data-ttu-id="adfbe-147">Only VMs created by the user</span><span class="sxs-lookup"><span data-stu-id="adfbe-147">Only VMs created by the user</span></span> |<span data-ttu-id="adfbe-148">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-148">Yes</span></span> |<span data-ttu-id="adfbe-149">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-149">Yes</span></span> |
| <span data-ttu-id="adfbe-150">Update VM policies</span><span class="sxs-lookup"><span data-stu-id="adfbe-150">Update VM policies</span></span> |<span data-ttu-id="adfbe-151">No</span><span class="sxs-lookup"><span data-stu-id="adfbe-151">No</span></span> |<span data-ttu-id="adfbe-152">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-152">Yes</span></span> |<span data-ttu-id="adfbe-153">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-153">Yes</span></span> |
| <span data-ttu-id="adfbe-154">Add/remove data disks to/from VMs</span><span class="sxs-lookup"><span data-stu-id="adfbe-154">Add/remove data disks to/from VMs</span></span> |<span data-ttu-id="adfbe-155">Only VMs created by the user</span><span class="sxs-lookup"><span data-stu-id="adfbe-155">Only VMs created by the user</span></span> |<span data-ttu-id="adfbe-156">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-156">Yes</span></span> |<span data-ttu-id="adfbe-157">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-157">Yes</span></span> |
| <span data-ttu-id="adfbe-158">**Artifact tasks**</span><span class="sxs-lookup"><span data-stu-id="adfbe-158">**Artifact tasks**</span></span> | | | |
| <span data-ttu-id="adfbe-159">Add and remove artifact repositories</span><span class="sxs-lookup"><span data-stu-id="adfbe-159">Add and remove artifact repositories</span></span> |<span data-ttu-id="adfbe-160">No</span><span class="sxs-lookup"><span data-stu-id="adfbe-160">No</span></span> |<span data-ttu-id="adfbe-161">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-161">Yes</span></span> |<span data-ttu-id="adfbe-162">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-162">Yes</span></span> |
| <span data-ttu-id="adfbe-163">Apply artifacts</span><span class="sxs-lookup"><span data-stu-id="adfbe-163">Apply artifacts</span></span> |<span data-ttu-id="adfbe-164">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-164">Yes</span></span> |<span data-ttu-id="adfbe-165">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-165">Yes</span></span> |<span data-ttu-id="adfbe-166">Yes</span><span class="sxs-lookup"><span data-stu-id="adfbe-166">Yes</span></span> |

> [!NOTE]
> <span data-ttu-id="adfbe-167">When a user creates a VM, that user is automatically assigned to the **Owner** role of the created VM.</span><span class="sxs-lookup"><span data-stu-id="adfbe-167">When a user creates a VM, that user is automatically assigned to the **Owner** role of the created VM.</span></span>
> 
> 

## <a name="add-an-owner-or-user-at-the-lab-level"></a><span data-ttu-id="adfbe-168">Add an owner or user at the lab level</span><span class="sxs-lookup"><span data-stu-id="adfbe-168">Add an owner or user at the lab level</span></span>
<span data-ttu-id="adfbe-169">Owners and users can be added at the lab level via the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="adfbe-169">Owners and users can be added at the lab level via the Azure portal.</span></span> <span data-ttu-id="adfbe-170">A user can be an external user with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="adfbe-170">A user can be an external user with a valid [Microsoft account (MSA)](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span>
<span data-ttu-id="adfbe-171">The following steps guide you through the process of adding an owner or user to a lab in Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="adfbe-171">The following steps guide you through the process of adding an owner or user to a lab in Azure DevTest Labs:</span></span>

1. <span data-ttu-id="adfbe-172">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="adfbe-172">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="adfbe-173">Select **All services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="adfbe-173">Select **All services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="adfbe-174">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="adfbe-174">From the list of labs, select the desired lab.</span></span>
4. <span data-ttu-id="adfbe-175">On the lab's blade, select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-175">On the lab's blade, select **Configuration and policies**.</span></span> 
5. <span data-ttu-id="adfbe-176">On the **Configuration and policies** page, select **Access control (IAM)** from the menu on the left.</span><span class="sxs-lookup"><span data-stu-id="adfbe-176">On the **Configuration and policies** page, select **Access control (IAM)** from the menu on the left.</span></span> 
6. <span data-ttu-id="adfbe-177">Select **Add** on the toolbar to add a user to a role.</span><span class="sxs-lookup"><span data-stu-id="adfbe-177">Select **Add** on the toolbar to add a user to a role.</span></span>

    ![Add user](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
1. <span data-ttu-id="adfbe-179">In the **Add permissions** window, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="adfbe-179">In the **Add permissions** window, do the following actions:</span></span> 
    1. <span data-ttu-id="adfbe-180">Select a role (for example: DevTest Labs User).</span><span class="sxs-lookup"><span data-stu-id="adfbe-180">Select a role (for example: DevTest Labs User).</span></span> <span data-ttu-id="adfbe-181">The section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists the various actions that can be performed by users in the Owner, DevTest User, and Contributor roles.</span><span class="sxs-lookup"><span data-stu-id="adfbe-181">The section [Actions that can be performed in each role](#actions-that-can-be-performed-in-each-role) lists the various actions that can be performed by users in the Owner, DevTest User, and Contributor roles.</span></span>
    2. <span data-ttu-id="adfbe-182">Select the user to be added to the role.</span><span class="sxs-lookup"><span data-stu-id="adfbe-182">Select the user to be added to the role.</span></span> 
    3. <span data-ttu-id="adfbe-183">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-183">Select **Save**.</span></span> 

        ![Add user to the role](./media/devtest-lab-add-devtest-user/add-user.png) 
11. <span data-ttu-id="adfbe-185">When you return to the **Users** blade, the user has been added.</span><span class="sxs-lookup"><span data-stu-id="adfbe-185">When you return to the **Users** blade, the user has been added.</span></span>  

## <a name="add-an-external-user-to-a-lab-using-powershell"></a><span data-ttu-id="adfbe-186">Add an external user to a lab using PowerShell</span><span class="sxs-lookup"><span data-stu-id="adfbe-186">Add an external user to a lab using PowerShell</span></span>
<span data-ttu-id="adfbe-187">In addition to adding users in the Azure portal, you can add an external user to your lab using a PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="adfbe-187">In addition to adding users in the Azure portal, you can add an external user to your lab using a PowerShell script.</span></span> <span data-ttu-id="adfbe-188">In the following example, modify the parameter values under the **Values to change** comment.</span><span class="sxs-lookup"><span data-stu-id="adfbe-188">In the following example, modify the parameter values under the **Values to change** comment.</span></span>
<span data-ttu-id="adfbe-189">You can retrieve the `subscriptionId`, `labResourceGroup`, and `labName` values from the lab blade in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="adfbe-189">You can retrieve the `subscriptionId`, `labResourceGroup`, and `labName` values from the lab blade in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="adfbe-190">The sample script assumes that the specified user has been added as a guest to the Active Directory, and will fail if that is not the case.</span><span class="sxs-lookup"><span data-stu-id="adfbe-190">The sample script assumes that the specified user has been added as a guest to the Active Directory, and will fail if that is not the case.</span></span> <span data-ttu-id="adfbe-191">To add a user not in the Active Directory to a lab, use the Azure portal to assign the user to a role as illustrated in the section, [Add an owner or user at the lab level](#add-an-owner-or-user-at-the-lab-level).</span><span class="sxs-lookup"><span data-stu-id="adfbe-191">To add a user not in the Active Directory to a lab, use the Azure portal to assign the user to a role as illustrated in the section, [Add an owner or user at the lab level](#add-an-owner-or-user-at-the-lab-level).</span></span>   
> 
> 

    # Add an external user in DevTest Labs user role to a lab
    # Ensure that guest users can be added to the Azure Active directory:
    # https://azure.microsoft.com/documentation/articles/active-directory-create-users/#set-guest-user-access-policies

    # Values to change
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource name here>"
    $labName = "<Enter lab name here>"
    $userDisplayName = "<Enter user's display name here>"

    # Log into your Azure account
    Connect-AzureRmAccount

    # Select the Azure subscription that contains the lab. 
    # This step is optional if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Retrieve the user object
    $adObject = Get-AzureRmADUser -SearchString $userDisplayName

    # Create the role assignment. 
    $labId = ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    New-AzureRmRoleAssignment -ObjectId $adObject.Id -RoleDefinitionName 'DevTest Labs User' -Scope $labId

## <a name="add-an-owner-or-user-at-the-subscription-level"></a><span data-ttu-id="adfbe-192">Add an owner or user at the subscription level</span><span class="sxs-lookup"><span data-stu-id="adfbe-192">Add an owner or user at the subscription level</span></span>
<span data-ttu-id="adfbe-193">Azure permissions are propagated from parent scope to child scope in Azure.</span><span class="sxs-lookup"><span data-stu-id="adfbe-193">Azure permissions are propagated from parent scope to child scope in Azure.</span></span> <span data-ttu-id="adfbe-194">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span><span class="sxs-lookup"><span data-stu-id="adfbe-194">Therefore, owners of an Azure subscription that contains labs are automatically owners of those labs.</span></span> <span data-ttu-id="adfbe-195">They also own the VMs and other resources created by the lab's users, and the Azure DevTest Labs service.</span><span class="sxs-lookup"><span data-stu-id="adfbe-195">They also own the VMs and other resources created by the lab's users, and the Azure DevTest Labs service.</span></span> 

<span data-ttu-id="adfbe-196">You can add additional owners to a lab via the lab's blade in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="adfbe-196">You can add additional owners to a lab via the lab's blade in the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> <span data-ttu-id="adfbe-197">However, the added owner's scope of administration is more narrow than the subscription owner's scope.</span><span class="sxs-lookup"><span data-stu-id="adfbe-197">However, the added owner's scope of administration is more narrow than the subscription owner's scope.</span></span> <span data-ttu-id="adfbe-198">For example, the added owners do not have full access to some of the resources that are created in the subscription by the DevTest Labs service.</span><span class="sxs-lookup"><span data-stu-id="adfbe-198">For example, the added owners do not have full access to some of the resources that are created in the subscription by the DevTest Labs service.</span></span> 

<span data-ttu-id="adfbe-199">To add an owner to an Azure subscription, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="adfbe-199">To add an owner to an Azure subscription, follow these steps:</span></span>

1. <span data-ttu-id="adfbe-200">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="adfbe-200">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="adfbe-201">Select **All Services**, and then select **Subscriptions** from the list.</span><span class="sxs-lookup"><span data-stu-id="adfbe-201">Select **All Services**, and then select **Subscriptions** from the list.</span></span>
3. <span data-ttu-id="adfbe-202">Select the desired subscription.</span><span class="sxs-lookup"><span data-stu-id="adfbe-202">Select the desired subscription.</span></span>
4. <span data-ttu-id="adfbe-203">Select **Access** icon.</span><span class="sxs-lookup"><span data-stu-id="adfbe-203">Select **Access** icon.</span></span> 
   
    ![Access users](./media/devtest-lab-add-devtest-user/access-users.png)
5. <span data-ttu-id="adfbe-205">On the **Users** blade, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-205">On the **Users** blade, select **Add**.</span></span>
   
    ![Add user](./media/devtest-lab-add-devtest-user/devtest-users-blade.png)
6. <span data-ttu-id="adfbe-207">On the **Select a role** blade, select **Owner**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-207">On the **Select a role** blade, select **Owner**.</span></span>
7. <span data-ttu-id="adfbe-208">On the **Add users** blade, enter the email address or name of the user you want to add as an owner.</span><span class="sxs-lookup"><span data-stu-id="adfbe-208">On the **Add users** blade, enter the email address or name of the user you want to add as an owner.</span></span> <span data-ttu-id="adfbe-209">If the user can't be found, you get an error message explaining the issue.</span><span class="sxs-lookup"><span data-stu-id="adfbe-209">If the user can't be found, you get an error message explaining the issue.</span></span> <span data-ttu-id="adfbe-210">If the user is found, that user is listed under the **User** text box.</span><span class="sxs-lookup"><span data-stu-id="adfbe-210">If the user is found, that user is listed under the **User** text box.</span></span>
8. <span data-ttu-id="adfbe-211">Select the located user name.</span><span class="sxs-lookup"><span data-stu-id="adfbe-211">Select the located user name.</span></span>
9. <span data-ttu-id="adfbe-212">Select **Select**.</span><span class="sxs-lookup"><span data-stu-id="adfbe-212">Select **Select**.</span></span>
10. <span data-ttu-id="adfbe-213">Select **OK** to close the **Add access** blade.</span><span class="sxs-lookup"><span data-stu-id="adfbe-213">Select **OK** to close the **Add access** blade.</span></span>
11. <span data-ttu-id="adfbe-214">When you return to the **Users** blade, the user has been added as an owner.</span><span class="sxs-lookup"><span data-stu-id="adfbe-214">When you return to the **Users** blade, the user has been added as an owner.</span></span> <span data-ttu-id="adfbe-215">This user is now an owner of any labs created under this subscription, and thus is able to perform owner tasks.</span><span class="sxs-lookup"><span data-stu-id="adfbe-215">This user is now an owner of any labs created under this subscription, and thus is able to perform owner tasks.</span></span> 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

