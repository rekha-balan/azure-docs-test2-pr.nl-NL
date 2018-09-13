---
title: How to migrate your individual licensed users to a group  in Azure Active Directory | Microsoft Docs
description: How to switch from individual user licenses to group-based licensing using Azure Active Directory
services: active-directory
keywords: Azure AD licensing
documentationcenter: ''
author: curtand
manager: femila
editor: ''
ms.assetid: ''
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/28/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 431f72e45732aaf11dab1dc1686e4a2b3940946f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660551"
---
# <a name="how-to-add-licensed-users-to-a-group-for-licensing-in-azure-active-directory"></a><span data-ttu-id="426e3-104">How to add licensed users to a group for licensing in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="426e3-104">How to add licensed users to a group for licensing in Azure Active Directory</span></span>

<span data-ttu-id="426e3-105">You may have existing licenses deployed to users in the organizations via “direct assignment”; that is, using PowerShell scripts or other tools to assign individual user licenses.</span><span class="sxs-lookup"><span data-stu-id="426e3-105">You may have existing licenses deployed to users in the organizations via “direct assignment”; that is, using PowerShell scripts or other tools to assign individual user licenses.</span></span> <span data-ttu-id="426e3-106">If you would like to start using group-based licensing to manage licenses in your organization, you will need a migration plan to seamlessly replace existing solutions with group-based licensing.</span><span class="sxs-lookup"><span data-stu-id="426e3-106">If you would like to start using group-based licensing to manage licenses in your organization, you will need a migration plan to seamlessly replace existing solutions with group-based licensing.</span></span>

<span data-ttu-id="426e3-107">The most important thing to keep in mind is that you should avoid a situation where migrating to group-based licensing will result in users temporarily losing their currently assigned licenses.</span><span class="sxs-lookup"><span data-stu-id="426e3-107">The most important thing to keep in mind is that you should avoid a situation where migrating to group-based licensing will result in users temporarily losing their currently assigned licenses.</span></span> <span data-ttu-id="426e3-108">Any process that may result in removal of licenses should be avoided to remove the risk of users losing access to services and their data.</span><span class="sxs-lookup"><span data-stu-id="426e3-108">Any process that may result in removal of licenses should be avoided to remove the risk of users losing access to services and their data.</span></span>

## <a name="recommended-migration-process"></a><span data-ttu-id="426e3-109">Recommended migration process</span><span class="sxs-lookup"><span data-stu-id="426e3-109">Recommended migration process</span></span>

1. <span data-ttu-id="426e3-110">You have existing automation (for example, PowerShell) managing license assignment and removal for users.</span><span class="sxs-lookup"><span data-stu-id="426e3-110">You have existing automation (for example, PowerShell) managing license assignment and removal for users.</span></span> <span data-ttu-id="426e3-111">Leave it running as is.</span><span class="sxs-lookup"><span data-stu-id="426e3-111">Leave it running as is.</span></span>

2. <span data-ttu-id="426e3-112">Create a new licensing group (or decide which existing groups to use) and make sure that all required users are added as members.</span><span class="sxs-lookup"><span data-stu-id="426e3-112">Create a new licensing group (or decide which existing groups to use) and make sure that all required users are added as members.</span></span>

3. <span data-ttu-id="426e3-113">Assign the required licenses to those groups; your goal should be to reflect the same licensing state your existing automation (for example, PowerShell) is applying to those users.</span><span class="sxs-lookup"><span data-stu-id="426e3-113">Assign the required licenses to those groups; your goal should be to reflect the same licensing state your existing automation (for example, PowerShell) is applying to those users.</span></span>

4. <span data-ttu-id="426e3-114">Verify that licenses have been applied to all users in those groups.</span><span class="sxs-lookup"><span data-stu-id="426e3-114">Verify that licenses have been applied to all users in those groups.</span></span> <span data-ttu-id="426e3-115">This can be done by checking the processing state on each group and by checking Audit Logs.</span><span class="sxs-lookup"><span data-stu-id="426e3-115">This can be done by checking the processing state on each group and by checking Audit Logs.</span></span>

  - <span data-ttu-id="426e3-116">You can spot check individual users by looking at their license details.</span><span class="sxs-lookup"><span data-stu-id="426e3-116">You can spot check individual users by looking at their license details.</span></span> <span data-ttu-id="426e3-117">You will see that they have the same licenses assigned “directly” and “inherited” from groups.</span><span class="sxs-lookup"><span data-stu-id="426e3-117">You will see that they have the same licenses assigned “directly” and “inherited” from groups.</span></span>

  - <span data-ttu-id="426e3-118">You can run a PowerShell script to [verify how licenses are assigned to users](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span><span class="sxs-lookup"><span data-stu-id="426e3-118">You can run a PowerShell script to [verify how licenses are assigned to users](active-directory-licensing-group-advanced.md#use-powershell-to-see-who-has-inherited-and-direct-licenses).</span></span>

  - <span data-ttu-id="426e3-119">When the same product license is assigned to the user both directly and through a group, only one license is consumed by the user.</span><span class="sxs-lookup"><span data-stu-id="426e3-119">When the same product license is assigned to the user both directly and through a group, only one license is consumed by the user.</span></span> <span data-ttu-id="426e3-120">Hence no additional licenses are required to perform migration.</span><span class="sxs-lookup"><span data-stu-id="426e3-120">Hence no additional licenses are required to perform migration.</span></span>

5. <span data-ttu-id="426e3-121">Verify that no license assignments failed by checking each group for users in error state.</span><span class="sxs-lookup"><span data-stu-id="426e3-121">Verify that no license assignments failed by checking each group for users in error state.</span></span> <span data-ttu-id="426e3-122">For more information, see [Identifying and resolving license problems for a group](active-directory-licensing-group-problem-resolution-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="426e3-122">For more information, see [Identifying and resolving license problems for a group](active-directory-licensing-group-problem-resolution-azure-portal.md).</span></span>

6. <span data-ttu-id="426e3-123">Consider removing the original direct assignments; you may want to do it gradually, in “waves”, to monitor the outcome on a subset of users first.</span><span class="sxs-lookup"><span data-stu-id="426e3-123">Consider removing the original direct assignments; you may want to do it gradually, in “waves”, to monitor the outcome on a subset of users first.</span></span>

  <span data-ttu-id="426e3-124">You could leave the original direct assignments on users, but when the users leave their licensed groups they will still retain the original license, which is possibly not want you want.</span><span class="sxs-lookup"><span data-stu-id="426e3-124">You could leave the original direct assignments on users, but when the users leave their licensed groups they will still retain the original license, which is possibly not want you want.</span></span>

## <a name="an-example"></a><span data-ttu-id="426e3-125">An example</span><span class="sxs-lookup"><span data-stu-id="426e3-125">An example</span></span>

<span data-ttu-id="426e3-126">We have an organization with 1,000 users.</span><span class="sxs-lookup"><span data-stu-id="426e3-126">We have an organization with 1,000 users.</span></span> <span data-ttu-id="426e3-127">All users require Enterprise Mobility + Security (EMS) licenses.</span><span class="sxs-lookup"><span data-stu-id="426e3-127">All users require Enterprise Mobility + Security (EMS) licenses.</span></span> <span data-ttu-id="426e3-128">200 users are in the Finance Department and require Office 365 Enterprise E3 licenses.</span><span class="sxs-lookup"><span data-stu-id="426e3-128">200 users are in the Finance Department and require Office 365 Enterprise E3 licenses.</span></span> <span data-ttu-id="426e3-129">We have a PowerShell script running on premises adding and removing licenses from users as they come and go.</span><span class="sxs-lookup"><span data-stu-id="426e3-129">We have a PowerShell script running on premises adding and removing licenses from users as they come and go.</span></span> <span data-ttu-id="426e3-130">We want to replace the script with group-based licensing so licenses are managed automatically by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="426e3-130">We want to replace the script with group-based licensing so licenses are managed automatically by Azure AD.</span></span>

<span data-ttu-id="426e3-131">Here is what the migration process could look like:</span><span class="sxs-lookup"><span data-stu-id="426e3-131">Here is what the migration process could look like:</span></span>

1. <span data-ttu-id="426e3-132">Using the Azure portal assign the EMS license to the **All users** group in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="426e3-132">Using the Azure portal assign the EMS license to the **All users** group in Azure AD.</span></span> <span data-ttu-id="426e3-133">Assign the E3 license to the **Finance department** group that contains all the required users.</span><span class="sxs-lookup"><span data-stu-id="426e3-133">Assign the E3 license to the **Finance department** group that contains all the required users.</span></span>

2. <span data-ttu-id="426e3-134">For each group, confirm that license assignment has completed for all users.</span><span class="sxs-lookup"><span data-stu-id="426e3-134">For each group, confirm that license assignment has completed for all users.</span></span> <span data-ttu-id="426e3-135">Go to the blade for each group, select **Licenses**, and check the processing status at the top of the **Licenses** blade.</span><span class="sxs-lookup"><span data-stu-id="426e3-135">Go to the blade for each group, select **Licenses**, and check the processing status at the top of the **Licenses** blade.</span></span>

  - <span data-ttu-id="426e3-136">Look for “Latest license changes have been applied to all users" to confirm processing has completed.</span><span class="sxs-lookup"><span data-stu-id="426e3-136">Look for “Latest license changes have been applied to all users" to confirm processing has completed.</span></span>

  - <span data-ttu-id="426e3-137">Look for a notification on top about any users for whom licenses may have not been successfully assigned.</span><span class="sxs-lookup"><span data-stu-id="426e3-137">Look for a notification on top about any users for whom licenses may have not been successfully assigned.</span></span> <span data-ttu-id="426e3-138">Did we run out of licenses for some users?</span><span class="sxs-lookup"><span data-stu-id="426e3-138">Did we run out of licenses for some users?</span></span> <span data-ttu-id="426e3-139">Do some users have conflicting license SKUs that prevent them from inheriting group licenses?</span><span class="sxs-lookup"><span data-stu-id="426e3-139">Do some users have conflicting license SKUs that prevent them from inheriting group licenses?</span></span>

3. <span data-ttu-id="426e3-140">Spot check some users to verify that they have both the direct and group licenses applied.</span><span class="sxs-lookup"><span data-stu-id="426e3-140">Spot check some users to verify that they have both the direct and group licenses applied.</span></span> <span data-ttu-id="426e3-141">Go to the blade for a user, select **Licenses**, and examine the state of licenses.</span><span class="sxs-lookup"><span data-stu-id="426e3-141">Go to the blade for a user, select **Licenses**, and examine the state of licenses.</span></span>

  - <span data-ttu-id="426e3-142">This is the expected user state during migration:</span><span class="sxs-lookup"><span data-stu-id="426e3-142">This is the expected user state during migration:</span></span>

      ![expected user state](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-migration-azure-portal/expected-user-state.png)

  <span data-ttu-id="426e3-144">This confirms that the user has both direct and inherited licenses.</span><span class="sxs-lookup"><span data-stu-id="426e3-144">This confirms that the user has both direct and inherited licenses.</span></span> <span data-ttu-id="426e3-145">We see that both **EMS** and **E3** are assigned.</span><span class="sxs-lookup"><span data-stu-id="426e3-145">We see that both **EMS** and **E3** are assigned.</span></span>

  - <span data-ttu-id="426e3-146">Select each license to show details about the enabled services.</span><span class="sxs-lookup"><span data-stu-id="426e3-146">Select each license to show details about the enabled services.</span></span> <span data-ttu-id="426e3-147">This can be used to check if the direct and group licenses enable exactly the same service plans for the user.</span><span class="sxs-lookup"><span data-stu-id="426e3-147">This can be used to check if the direct and group licenses enable exactly the same service plans for the user.</span></span>

      ![check service plans](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-migration-azure-portal/check-service-plans.png)

4. <span data-ttu-id="426e3-149">After confirming that both direct and group licenses are equivalent, you can start removing direct licenses from users.</span><span class="sxs-lookup"><span data-stu-id="426e3-149">After confirming that both direct and group licenses are equivalent, you can start removing direct licenses from users.</span></span> <span data-ttu-id="426e3-150">You can test this by removing them for individual users in the portal and then run automation scripts to have them removed in bulk.</span><span class="sxs-lookup"><span data-stu-id="426e3-150">You can test this by removing them for individual users in the portal and then run automation scripts to have them removed in bulk.</span></span> <span data-ttu-id="426e3-151">Here is an example of the same user with the direct licenses removed through the portal.</span><span class="sxs-lookup"><span data-stu-id="426e3-151">Here is an example of the same user with the direct licenses removed through the portal.</span></span> <span data-ttu-id="426e3-152">Notice that the license state remains unchanged, but we no longer see direct assignments.</span><span class="sxs-lookup"><span data-stu-id="426e3-152">Notice that the license state remains unchanged, but we no longer see direct assignments.</span></span>

  ![direct licenses removed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-licensing-group-migration-azure-portal/direct-licenses-removed.png)


## <a name="next-steps"></a><span data-ttu-id="426e3-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="426e3-154">Next steps</span></span>

<span data-ttu-id="426e3-155">To learn more about other scenarios for license management through groups, read</span><span class="sxs-lookup"><span data-stu-id="426e3-155">To learn more about other scenarios for license management through groups, read</span></span>

* [<span data-ttu-id="426e3-156">Assigning licenses to a group in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="426e3-156">Assigning licenses to a group in Azure Active Directory</span></span>](active-directory-licensing-group-assignment-azure-portal.md)
* [<span data-ttu-id="426e3-157">What is group-based licensing in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="426e3-157">What is group-based licensing in Azure Active Directory?</span></span>](active-directory-licensing-whatis-azure-portal.md)
* [<span data-ttu-id="426e3-158">Identifying and resolving license problems for a group in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="426e3-158">Identifying and resolving license problems for a group in Azure Active Directory</span></span>](active-directory-licensing-group-problem-resolution-azure-portal.md)
* [<span data-ttu-id="426e3-159">Azure Active Directory group-based licensing additional scenarios</span><span class="sxs-lookup"><span data-stu-id="426e3-159">Azure Active Directory group-based licensing additional scenarios</span></span>](active-directory-licensing-group-advanced.md)



