---
title: Migrate user licenses users to group-based licensing in Azure Active Directory | Microsoft Docs
description: How to switch from individual user licenses to group-based licensing using Azure Active Directory
services: active-directory
keywords: Azure AD licensing
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: article
ms.workload: identity
ms.component: users-groups-roles
ms.date: 01/14/2018
ms.author: curtand
ms.custom: seohack1
ms.openlocfilehash: 10851990f26124ae89945d4b56058115cacb81ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855770"
---
# <a name="how-to-add-licensed-users-to-a-group-for-licensing-in-azure-active-directory"></a><span data-ttu-id="608c4-104">How to add licensed users to a group for licensing in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="608c4-104">How to add licensed users to a group for licensing in Azure Active Directory</span></span>

<span data-ttu-id="608c4-105">You may have existing licenses deployed to users in the organizations via “direct assignment”; that is, using PowerShell scripts or other tools to assign individual user licenses.</span><span class="sxs-lookup"><span data-stu-id="608c4-105">You may have existing licenses deployed to users in the organizations via “direct assignment”; that is, using PowerShell scripts or other tools to assign individual user licenses.</span></span> <span data-ttu-id="608c4-106">If you would like to start using group-based licensing to manage licenses in your organization, you will need a migration plan to seamlessly replace existing solutions with group-based licensing.</span><span class="sxs-lookup"><span data-stu-id="608c4-106">If you would like to start using group-based licensing to manage licenses in your organization, you will need a migration plan to seamlessly replace existing solutions with group-based licensing.</span></span>

<span data-ttu-id="608c4-107">The most important thing to keep in mind is that you should avoid a situation where migrating to group-based licensing will result in users temporarily losing their currently assigned licenses.</span><span class="sxs-lookup"><span data-stu-id="608c4-107">The most important thing to keep in mind is that you should avoid a situation where migrating to group-based licensing will result in users temporarily losing their currently assigned licenses.</span></span> <span data-ttu-id="608c4-108">Any process that may result in removal of licenses should be avoided to remove the risk of users losing access to services and their data.</span><span class="sxs-lookup"><span data-stu-id="608c4-108">Any process that may result in removal of licenses should be avoided to remove the risk of users losing access to services and their data.</span></span>

## <a name="recommended-migration-process"></a><span data-ttu-id="608c4-109">Recommended migration process</span><span class="sxs-lookup"><span data-stu-id="608c4-109">Recommended migration process</span></span>

1. <span data-ttu-id="608c4-110">You have existing automation (for example, PowerShell) managing license assignment and removal for users.</span><span class="sxs-lookup"><span data-stu-id="608c4-110">You have existing automation (for example, PowerShell) managing license assignment and removal for users.</span></span> <span data-ttu-id="608c4-111">Leave it running as is.</span><span class="sxs-lookup"><span data-stu-id="608c4-111">Leave it running as is.</span></span>

2. <span data-ttu-id="608c4-112">Create a new licensing group (or decide which existing groups to use) and make sure that all required users are added as members.</span><span class="sxs-lookup"><span data-stu-id="608c4-112">Create a new licensing group (or decide which existing groups to use) and make sure that all required users are added as members.</span></span>

3. <span data-ttu-id="608c4-113">Assign the required licenses to those groups; your goal should be to reflect the same licensing state your existing automation (for example, PowerShell) is applying to those users.</span><span class="sxs-lookup"><span data-stu-id="608c4-113">Assign the required licenses to those groups; your goal should be to reflect the same licensing state your existing automation (for example, PowerShell) is applying to those users.</span></span>

4. <span data-ttu-id="608c4-114">Verify that licenses have been applied to all users in those groups.</span><span class="sxs-lookup"><span data-stu-id="608c4-114">Verify that licenses have been applied to all users in those groups.</span></span> <span data-ttu-id="608c4-115">This application can be done by checking the processing state on each group and by checking Audit Logs.</span><span class="sxs-lookup"><span data-stu-id="608c4-115">This application can be done by checking the processing state on each group and by checking Audit Logs.</span></span>

  - <span data-ttu-id="608c4-116">You can spot check individual users by looking at their license details.</span><span class="sxs-lookup"><span data-stu-id="608c4-116">You can spot check individual users by looking at their license details.</span></span> <span data-ttu-id="608c4-117">You will see that they have the same licenses assigned “directly” and “inherited” from groups.</span><span class="sxs-lookup"><span data-stu-id="608c4-117">You will see that they have the same licenses assigned “directly” and “inherited” from groups.</span></span>

  - <span data-ttu-id="608c4-118">You can run a PowerShell script to [verify how licenses are assigned to users](licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span><span class="sxs-lookup"><span data-stu-id="608c4-118">You can run a PowerShell script to [verify how licenses are assigned to users](licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span></span>

  - <span data-ttu-id="608c4-119">When the same product license is assigned to the user both directly and through a group, only one license is consumed by the user.</span><span class="sxs-lookup"><span data-stu-id="608c4-119">When the same product license is assigned to the user both directly and through a group, only one license is consumed by the user.</span></span> <span data-ttu-id="608c4-120">Hence no additional licenses are required to perform migration.</span><span class="sxs-lookup"><span data-stu-id="608c4-120">Hence no additional licenses are required to perform migration.</span></span>

5. <span data-ttu-id="608c4-121">Verify that no license assignments failed by checking each group for users in error state.</span><span class="sxs-lookup"><span data-stu-id="608c4-121">Verify that no license assignments failed by checking each group for users in error state.</span></span> <span data-ttu-id="608c4-122">For more information, see [Identifying and resolving license problems for a group](licensing-groups-resolve-problems.md).</span><span class="sxs-lookup"><span data-stu-id="608c4-122">For more information, see [Identifying and resolving license problems for a group](licensing-groups-resolve-problems.md).</span></span>

6. <span data-ttu-id="608c4-123">Consider removing the original direct assignments; you may want to do it gradually, in “waves”, to monitor the outcome on a subset of users first.</span><span class="sxs-lookup"><span data-stu-id="608c4-123">Consider removing the original direct assignments; you may want to do it gradually, in “waves”, to monitor the outcome on a subset of users first.</span></span>

  <span data-ttu-id="608c4-124">You could leave the original direct assignments on users, but when the users leave their licensed groups they will still retain the original license, which is possibly not want you want.</span><span class="sxs-lookup"><span data-stu-id="608c4-124">You could leave the original direct assignments on users, but when the users leave their licensed groups they will still retain the original license, which is possibly not want you want.</span></span>

## <a name="an-example"></a><span data-ttu-id="608c4-125">An example</span><span class="sxs-lookup"><span data-stu-id="608c4-125">An example</span></span>

<span data-ttu-id="608c4-126">An organization has 1,000 users.</span><span class="sxs-lookup"><span data-stu-id="608c4-126">An organization has 1,000 users.</span></span> <span data-ttu-id="608c4-127">All users require Enterprise Mobility + Security (EMS) licenses.</span><span class="sxs-lookup"><span data-stu-id="608c4-127">All users require Enterprise Mobility + Security (EMS) licenses.</span></span> <span data-ttu-id="608c4-128">200 users are in the Finance Department and require Office 365 Enterprise E3 licenses.</span><span class="sxs-lookup"><span data-stu-id="608c4-128">200 users are in the Finance Department and require Office 365 Enterprise E3 licenses.</span></span> <span data-ttu-id="608c4-129">Currently the organization has a PowerShell script running on premises, adding and removing licenses from users as they come and go.</span><span class="sxs-lookup"><span data-stu-id="608c4-129">Currently the organization has a PowerShell script running on premises, adding and removing licenses from users as they come and go.</span></span> <span data-ttu-id="608c4-130">However, the organization wants to replace the script with group-based licensing so licenses can be managed automatically by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="608c4-130">However, the organization wants to replace the script with group-based licensing so licenses can be managed automatically by Azure AD.</span></span>

<span data-ttu-id="608c4-131">Here is what the migration process could look like:</span><span class="sxs-lookup"><span data-stu-id="608c4-131">Here is what the migration process could look like:</span></span>

1. <span data-ttu-id="608c4-132">Using the Azure portal, assign the EMS license to the **All users** group in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="608c4-132">Using the Azure portal, assign the EMS license to the **All users** group in Azure AD.</span></span> <span data-ttu-id="608c4-133">Assign the E3 license to the **Finance department** group that contains all the required users.</span><span class="sxs-lookup"><span data-stu-id="608c4-133">Assign the E3 license to the **Finance department** group that contains all the required users.</span></span>

2. <span data-ttu-id="608c4-134">For each group, confirm that license assignment has completed for all users.</span><span class="sxs-lookup"><span data-stu-id="608c4-134">For each group, confirm that license assignment has completed for all users.</span></span> <span data-ttu-id="608c4-135">Go to the blade for each group, select **Licenses**, and check the processing status at the top of the **Licenses** blade.</span><span class="sxs-lookup"><span data-stu-id="608c4-135">Go to the blade for each group, select **Licenses**, and check the processing status at the top of the **Licenses** blade.</span></span>

  - <span data-ttu-id="608c4-136">Look for “Latest license changes have been applied to all users" to confirm processing has completed.</span><span class="sxs-lookup"><span data-stu-id="608c4-136">Look for “Latest license changes have been applied to all users" to confirm processing has completed.</span></span>

  - <span data-ttu-id="608c4-137">Look for a notification on top about any users for whom licenses may have not been successfully assigned.</span><span class="sxs-lookup"><span data-stu-id="608c4-137">Look for a notification on top about any users for whom licenses may have not been successfully assigned.</span></span> <span data-ttu-id="608c4-138">Did we run out of licenses for some users?</span><span class="sxs-lookup"><span data-stu-id="608c4-138">Did we run out of licenses for some users?</span></span> <span data-ttu-id="608c4-139">Do some users have conflicting license SKUs that prevent them from inheriting group licenses?</span><span class="sxs-lookup"><span data-stu-id="608c4-139">Do some users have conflicting license SKUs that prevent them from inheriting group licenses?</span></span>

3. <span data-ttu-id="608c4-140">Spot check some users to verify that they have both the direct and group licenses applied.</span><span class="sxs-lookup"><span data-stu-id="608c4-140">Spot check some users to verify that they have both the direct and group licenses applied.</span></span> <span data-ttu-id="608c4-141">Go to the blade for a user, select **Licenses**, and examine the state of licenses.</span><span class="sxs-lookup"><span data-stu-id="608c4-141">Go to the blade for a user, select **Licenses**, and examine the state of licenses.</span></span>

  - <span data-ttu-id="608c4-142">This is the expected user state during migration:</span><span class="sxs-lookup"><span data-stu-id="608c4-142">This is the expected user state during migration:</span></span>

      ![expected user state](./media/licensing-groups-migrate-users/expected-user-state.png)

  <span data-ttu-id="608c4-144">This confirms that the user has both direct and inherited licenses.</span><span class="sxs-lookup"><span data-stu-id="608c4-144">This confirms that the user has both direct and inherited licenses.</span></span> <span data-ttu-id="608c4-145">We see that both **EMS** and **E3** are assigned.</span><span class="sxs-lookup"><span data-stu-id="608c4-145">We see that both **EMS** and **E3** are assigned.</span></span>

  - <span data-ttu-id="608c4-146">Select each license to show details about the enabled services.</span><span class="sxs-lookup"><span data-stu-id="608c4-146">Select each license to show details about the enabled services.</span></span> <span data-ttu-id="608c4-147">This can be used to check if the direct and group licenses enable exactly the same service plans for the user.</span><span class="sxs-lookup"><span data-stu-id="608c4-147">This can be used to check if the direct and group licenses enable exactly the same service plans for the user.</span></span>

      ![check service plans](./media/licensing-groups-migrate-users/check-service-plans.png)

4. <span data-ttu-id="608c4-149">After confirming that both direct and group licenses are equivalent, you can start removing direct licenses from users.</span><span class="sxs-lookup"><span data-stu-id="608c4-149">After confirming that both direct and group licenses are equivalent, you can start removing direct licenses from users.</span></span> <span data-ttu-id="608c4-150">You can test this by removing them for individual users in the portal and then run automation scripts to have them removed in bulk.</span><span class="sxs-lookup"><span data-stu-id="608c4-150">You can test this by removing them for individual users in the portal and then run automation scripts to have them removed in bulk.</span></span> <span data-ttu-id="608c4-151">Here is an example of the same user with the direct licenses removed through the portal.</span><span class="sxs-lookup"><span data-stu-id="608c4-151">Here is an example of the same user with the direct licenses removed through the portal.</span></span> <span data-ttu-id="608c4-152">Notice that the license state remains unchanged, but we no longer see direct assignments.</span><span class="sxs-lookup"><span data-stu-id="608c4-152">Notice that the license state remains unchanged, but we no longer see direct assignments.</span></span>

  ![direct licenses removed](./media/licensing-groups-migrate-users/direct-licenses-removed.png)


## <a name="next-steps"></a><span data-ttu-id="608c4-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="608c4-154">Next steps</span></span>

<span data-ttu-id="608c4-155">To learn more about other scenarios for license management through groups, read</span><span class="sxs-lookup"><span data-stu-id="608c4-155">To learn more about other scenarios for license management through groups, read</span></span>

* [<span data-ttu-id="608c4-156">Assigning licenses to a group in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="608c4-156">Assigning licenses to a group in Azure Active Directory</span></span>](licensing-groups-assign.md)
* [<span data-ttu-id="608c4-157">What is group-based licensing in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="608c4-157">What is group-based licensing in Azure Active Directory?</span></span>](../fundamentals/active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="608c4-158">Identifying and resolving license problems for a group in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="608c4-158">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](licensing-groups-resolve-problems.md)
* [<span data-ttu-id="608c4-159">Azure Active Directory group-based licensing additional scenarios</span><span class="sxs-lookup"><span data-stu-id="608c4-159">Azure Active Directory group-based licensing additional scenarios</span></span>](licensing-group-advanced.md)
