---
title: Azure IoT Suite and Azure Active Directory | Microsoft Docs
description: Describes how Azure IoT Suite uses Azure Active Directory to manage permissions.
services: ''
suite: iot-suite
documentationcenter: ''
author: dominicbetts
manager: timlt
editor: ''
ms.assetid: 246228ba-954a-4d96-b6d6-e53e4590cb4f
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/02/2017
ms.author: dobett
ms.openlocfilehash: a56d535ee06a097c7c18bcd507c25708f6a33f91
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868513"
---
# <a name="permissions-on-the-azureiotsuitecom-site"></a><span data-ttu-id="70e3a-103">Permissions on the azureiotsuite.com site</span><span class="sxs-lookup"><span data-stu-id="70e3a-103">Permissions on the azureiotsuite.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="70e3a-104">What happens when you sign in</span><span class="sxs-lookup"><span data-stu-id="70e3a-104">What happens when you sign in</span></span>

<span data-ttu-id="70e3a-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="70e3a-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsuite], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="70e3a-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span><span class="sxs-lookup"><span data-stu-id="70e3a-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="70e3a-107">Currently, the site can only obtain user tokens for one tenant at a time.</span><span class="sxs-lookup"><span data-stu-id="70e3a-107">Currently, the site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="70e3a-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span><span class="sxs-lookup"><span data-stu-id="70e3a-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span></span>

2. <span data-ttu-id="70e3a-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span><span class="sxs-lookup"><span data-stu-id="70e3a-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span></span> <span data-ttu-id="70e3a-110">You see the available subscriptions when you create a new preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="70e3a-110">You see the available subscriptions when you create a new preconfigured solution.</span></span>

3. <span data-ttu-id="70e3a-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as preconfigured solutions and populates the tiles on the home page.</span><span class="sxs-lookup"><span data-stu-id="70e3a-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as preconfigured solutions and populates the tiles on the home page.</span></span>

<span data-ttu-id="70e3a-112">The following sections describe the roles that control access to the preconfigured solutions.</span><span class="sxs-lookup"><span data-stu-id="70e3a-112">The following sections describe the roles that control access to the preconfigured solutions.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="70e3a-113">AAD roles</span><span class="sxs-lookup"><span data-stu-id="70e3a-113">AAD roles</span></span>

<span data-ttu-id="70e3a-114">The AAD roles control the ability provision preconfigured solutions and manage users in a preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="70e3a-114">The AAD roles control the ability provision preconfigured solutions and manage users in a preconfigured solution.</span></span>

<span data-ttu-id="70e3a-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="70e3a-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="70e3a-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the preconfigured solutions.</span><span class="sxs-lookup"><span data-stu-id="70e3a-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the preconfigured solutions.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="70e3a-117">Global administrator</span><span class="sxs-lookup"><span data-stu-id="70e3a-117">Global administrator</span></span>

<span data-ttu-id="70e3a-118">There can be many global administrators per AAD tenant:</span><span class="sxs-lookup"><span data-stu-id="70e3a-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="70e3a-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span><span class="sxs-lookup"><span data-stu-id="70e3a-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span></span>
* <span data-ttu-id="70e3a-120">The global administrator can provision a preconfigured solution and is assigned an **Admin** role for the application inside their AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="70e3a-120">The global administrator can provision a preconfigured solution and is assigned an **Admin** role for the application inside their AAD tenant.</span></span>
* <span data-ttu-id="70e3a-121">If another user in the same AAD tenant creates an application, the default role granted to the global administrator is **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-121">If another user in the same AAD tenant creates an application, the default role granted to the global administrator is **ReadOnly**.</span></span>
* <span data-ttu-id="70e3a-122">A global administrator can assign users to roles for applications using the [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="70e3a-122">A global administrator can assign users to roles for applications using the [Azure portal][lnk-portal].</span></span>

### <a name="domain-user"></a><span data-ttu-id="70e3a-123">Domain user</span><span class="sxs-lookup"><span data-stu-id="70e3a-123">Domain user</span></span>

<span data-ttu-id="70e3a-124">There can be many domain users per AAD tenant:</span><span class="sxs-lookup"><span data-stu-id="70e3a-124">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="70e3a-125">A domain user can provision a preconfigured solution through the [azureiotsuite.com][lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="70e3a-125">A domain user can provision a preconfigured solution through the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="70e3a-126">By default, the domain user is granted the **Admin** role in the provisioned application.</span><span class="sxs-lookup"><span data-stu-id="70e3a-126">By default, the domain user is granted the **Admin** role in the provisioned application.</span></span>
* <span data-ttu-id="70e3a-127">A domain user can create an application using the build.cmd script in the [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span><span class="sxs-lookup"><span data-stu-id="70e3a-127">A domain user can create an application using the build.cmd script in the [azure-iot-remote-monitoring][lnk-rm-github-repo],  [azure-iot-predictive-maintenance][lnk-pm-github-repo], or [azure-iot-connected-factory][lnk-cf-github-repo] repository.</span></span> <span data-ttu-id="70e3a-128">However, the default role granted to the domain user is **ReadOnly**, because a domain user does not have permission to assign roles.</span><span class="sxs-lookup"><span data-stu-id="70e3a-128">However, the default role granted to the domain user is **ReadOnly**, because a domain user does not have permission to assign roles.</span></span>
* <span data-ttu-id="70e3a-129">If another user in the AAD tenant creates an application, the domain user is assigned the **ReadOnly** role by default for that application.</span><span class="sxs-lookup"><span data-stu-id="70e3a-129">If another user in the AAD tenant creates an application, the domain user is assigned the **ReadOnly** role by default for that application.</span></span>
* <span data-ttu-id="70e3a-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span><span class="sxs-lookup"><span data-stu-id="70e3a-130">A domain user cannot assign roles for applications; therefore a domain user cannot add users or roles for users for an application even if they provisioned it.</span></span>

### <a name="guest-user"></a><span data-ttu-id="70e3a-131">Guest User</span><span class="sxs-lookup"><span data-stu-id="70e3a-131">Guest User</span></span>

<span data-ttu-id="70e3a-132">There can be many guest users per AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="70e3a-132">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="70e3a-133">Guest users have a limited set of rights in the AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="70e3a-133">Guest users have a limited set of rights in the AAD tenant.</span></span> <span data-ttu-id="70e3a-134">As a result, guest users cannot provision a preconfigured solution in the AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="70e3a-134">As a result, guest users cannot provision a preconfigured solution in the AAD tenant.</span></span>

<span data-ttu-id="70e3a-135">For more information about users and roles in AAD, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="70e3a-135">For more information about users and roles in AAD, see the following resources:</span></span>

* <span data-ttu-id="70e3a-136">[Create users in Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="70e3a-136">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="70e3a-137">[Assign users to apps][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="70e3a-137">[Assign users to apps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="70e3a-138">Azure subscription administrator roles</span><span class="sxs-lookup"><span data-stu-id="70e3a-138">Azure subscription administrator roles</span></span>

<span data-ttu-id="70e3a-139">The Azure admin roles control the ability to map an Azure subscription to an AD tenant.</span><span class="sxs-lookup"><span data-stu-id="70e3a-139">The Azure admin roles control the ability to map an Azure subscription to an AD tenant.</span></span>

<span data-ttu-id="70e3a-140">Find out more about the Azure admin roles in the article [Add or change Azure subscription administrators][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="70e3a-140">Find out more about the Azure admin roles in the article [Add or change Azure subscription administrators][lnk-admin-roles].</span></span>

## <a name="application-roles"></a><span data-ttu-id="70e3a-141">Application roles</span><span class="sxs-lookup"><span data-stu-id="70e3a-141">Application roles</span></span>

<span data-ttu-id="70e3a-142">The application roles control access to devices in your preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="70e3a-142">The application roles control access to devices in your preconfigured solution.</span></span>

<span data-ttu-id="70e3a-143">There are two defined roles and one implicit role defined in a provisioned application:</span><span class="sxs-lookup"><span data-stu-id="70e3a-143">There are two defined roles and one implicit role defined in a provisioned application:</span></span>

* <span data-ttu-id="70e3a-144">**Admin:** Has full control to add, manage, remove devices, and modify settings.</span><span class="sxs-lookup"><span data-stu-id="70e3a-144">**Admin:** Has full control to add, manage, remove devices, and modify settings.</span></span>
* <span data-ttu-id="70e3a-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span><span class="sxs-lookup"><span data-stu-id="70e3a-145">**ReadOnly:** Can view devices, rules, actions, jobs, and telemetry.</span></span>

<span data-ttu-id="70e3a-146">You can find the permissions assigned to each role in the [RolePermissions.cs][lnk-resource-cs] source file.</span><span class="sxs-lookup"><span data-stu-id="70e3a-146">You can find the permissions assigned to each role in the [RolePermissions.cs][lnk-resource-cs] source file.</span></span>

### <a name="changing-application-roles-for-a-user"></a><span data-ttu-id="70e3a-147">Changing application roles for a user</span><span class="sxs-lookup"><span data-stu-id="70e3a-147">Changing application roles for a user</span></span>

<span data-ttu-id="70e3a-148">You can use the following procedure to make a user in your Active Directory an administrator of your preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="70e3a-148">You can use the following procedure to make a user in your Active Directory an administrator of your preconfigured solution.</span></span>

<span data-ttu-id="70e3a-149">You must be an AAD global administrator to change roles for a user:</span><span class="sxs-lookup"><span data-stu-id="70e3a-149">You must be an AAD global administrator to change roles for a user:</span></span>

1. <span data-ttu-id="70e3a-150">Go to the [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="70e3a-150">Go to the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="70e3a-151">Select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-151">Select **Azure Active Directory**.</span></span>
3. <span data-ttu-id="70e3a-152">Make sure you are using the directory you chose on azureiotsuite.com when you provisioned your solution.</span><span class="sxs-lookup"><span data-stu-id="70e3a-152">Make sure you are using the directory you chose on azureiotsuite.com when you provisioned your solution.</span></span> <span data-ttu-id="70e3a-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at the top-right of the portal.</span><span class="sxs-lookup"><span data-stu-id="70e3a-153">If you have multiple directories associated with your subscription, you can switch between them if you click your account name at the top-right of the portal.</span></span>
4. <span data-ttu-id="70e3a-154">Click **Enterprise applications**, then **All applications**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-154">Click **Enterprise applications**, then **All applications**.</span></span>
4. <span data-ttu-id="70e3a-155">Show **All applications** with **Any** status.</span><span class="sxs-lookup"><span data-stu-id="70e3a-155">Show **All applications** with **Any** status.</span></span> <span data-ttu-id="70e3a-156">Then search for an application with name of your preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="70e3a-156">Then search for an application with name of your preconfigured solution.</span></span>
5. <span data-ttu-id="70e3a-157">Click the name of the application that matches your preconfigured solution name.</span><span class="sxs-lookup"><span data-stu-id="70e3a-157">Click the name of the application that matches your preconfigured solution name.</span></span>
6. <span data-ttu-id="70e3a-158">Click **Users and groups**.</span><span class="sxs-lookup"><span data-stu-id="70e3a-158">Click **Users and groups**.</span></span>
7. <span data-ttu-id="70e3a-159">Select the user you want to switch roles.</span><span class="sxs-lookup"><span data-stu-id="70e3a-159">Select the user you want to switch roles.</span></span>
8. <span data-ttu-id="70e3a-160">Click **Assign** and select the role (such as **Admin**) you'd like to assign to the user, click the check mark.</span><span class="sxs-lookup"><span data-stu-id="70e3a-160">Click **Assign** and select the role (such as **Admin**) you'd like to assign to the user, click the check mark.</span></span>

## <a name="faq"></a><span data-ttu-id="70e3a-161">FAQ</span><span class="sxs-lookup"><span data-stu-id="70e3a-161">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="70e3a-162">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="70e3a-162">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="70e3a-163">How do I complete this task?</span><span class="sxs-lookup"><span data-stu-id="70e3a-163">How do I complete this task?</span></span>

<span data-ttu-id="70e3a-164">See [To add an existing subscription to your Azure AD directory](../active-directory/fundamentals/active-directory-how-subscriptions-associated-directory.md#to-associate-an-existing-subscription-to-your-azure-ad-directory)</span><span class="sxs-lookup"><span data-stu-id="70e3a-164">See [To add an existing subscription to your Azure AD directory](../active-directory/fundamentals/active-directory-how-subscriptions-associated-directory.md#to-associate-an-existing-subscription-to-your-azure-ad-directory)</span></span>

### <a name="im-a-domain-usermember-on-the-aad-tenant-and-ive-created-a-preconfigured-solution-how-do-i-get-assigned-a-role-for-my-application"></a><span data-ttu-id="70e3a-165">I'm a domain user/member on the AAD tenant and I've created a preconfigured solution.</span><span class="sxs-lookup"><span data-stu-id="70e3a-165">I'm a domain user/member on the AAD tenant and I've created a preconfigured solution.</span></span> <span data-ttu-id="70e3a-166">How do I get assigned a role for my application?</span><span class="sxs-lookup"><span data-stu-id="70e3a-166">How do I get assigned a role for my application?</span></span>

<span data-ttu-id="70e3a-167">Ask a global administrator to make you a global administrator on the AAD tenant and then assign roles to users yourself.</span><span class="sxs-lookup"><span data-stu-id="70e3a-167">Ask a global administrator to make you a global administrator on the AAD tenant and then assign roles to users yourself.</span></span> <span data-ttu-id="70e3a-168">Alternatively, ask a global administrator to assign you a role directly.</span><span class="sxs-lookup"><span data-stu-id="70e3a-168">Alternatively, ask a global administrator to assign you a role directly.</span></span> <span data-ttu-id="70e3a-169">If you'd like to change the AAD tenant your preconfigured solution has been deployed to, see the next question.</span><span class="sxs-lookup"><span data-stu-id="70e3a-169">If you'd like to change the AAD tenant your preconfigured solution has been deployed to, see the next question.</span></span>

### <a name="how-do-i-switch-the-aad-tenant-my-remote-monitoring-preconfigured-solution-and-application-are-assigned-to"></a><span data-ttu-id="70e3a-170">How do I switch the AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span><span class="sxs-lookup"><span data-stu-id="70e3a-170">How do I switch the AAD tenant my remote monitoring preconfigured solution and application are assigned to?</span></span>

<span data-ttu-id="70e3a-171">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="70e3a-171">You can run a cloud deployment from <https://github.com/Azure/azure-iot-remote-monitoring> and redeploy with a newly created AAD tenant.</span></span> <span data-ttu-id="70e3a-172">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions to add users and assign roles to those users.</span><span class="sxs-lookup"><span data-stu-id="70e3a-172">Because you are, by default, a global administrator when you create an AAD tenant, you have permissions to add users and assign roles to those users.</span></span>

1. <span data-ttu-id="70e3a-173">Create an AAD directory in the [Azure portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="70e3a-173">Create an AAD directory in the [Azure portal][lnk-portal].</span></span>
2. <span data-ttu-id="70e3a-174">Go to <https://github.com/Azure/azure-iot-remote-monitoring>.</span><span class="sxs-lookup"><span data-stu-id="70e3a-174">Go to <https://github.com/Azure/azure-iot-remote-monitoring>.</span></span>
3. <span data-ttu-id="70e3a-175">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span><span class="sxs-lookup"><span data-stu-id="70e3a-175">Run `build.cmd cloud [debug | release] {name of previously deployed remote monitoring solution}` (For example, `build.cmd cloud debug myRMSolution`)</span></span>
4. <span data-ttu-id="70e3a-176">When prompted, set the **tenantid** to be your newly created tenant instead of your previous tenant.</span><span class="sxs-lookup"><span data-stu-id="70e3a-176">When prompted, set the **tenantid** to be your newly created tenant instead of your previous tenant.</span></span>

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organisational-account"></a><span data-ttu-id="70e3a-177">I want to change a Service Administrator or Co-Administrator when logged in with an organisational account</span><span class="sxs-lookup"><span data-stu-id="70e3a-177">I want to change a Service Administrator or Co-Administrator when logged in with an organisational account</span></span>

<span data-ttu-id="70e3a-178">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="70e3a-178">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organisational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="70e3a-179">Why am I seeing this error?</span><span class="sxs-lookup"><span data-stu-id="70e3a-179">Why am I seeing this error?</span></span> <span data-ttu-id="70e3a-180">"Your account does not have the proper permissions to create a solution.</span><span class="sxs-lookup"><span data-stu-id="70e3a-180">"Your account does not have the proper permissions to create a solution.</span></span> <span data-ttu-id="70e3a-181">Please check with your account administrator or try with a different account."</span><span class="sxs-lookup"><span data-stu-id="70e3a-181">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="70e3a-182">Look at the following diagram for guidance:</span><span class="sxs-lookup"><span data-stu-id="70e3a-182">Look at the following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="70e3a-183">If you continue to see the error after validating you are a global administrator on the AAD tenant and a co-administrator on the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span><span class="sxs-lookup"><span data-stu-id="70e3a-183">If you continue to see the error after validating you are a global administrator on the AAD tenant and a co-administrator on the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="70e3a-184">First, add the user as a global administrator and then add user as a co-administrator on the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="70e3a-184">First, add the user as a global administrator and then add user as a co-administrator on the Azure subscription.</span></span> <span data-ttu-id="70e3a-185">If issues persist, contact [Help & Support][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="70e3a-185">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="70e3a-186">Why am I seeing this error when I have an Azure subscription?</span><span class="sxs-lookup"><span data-stu-id="70e3a-186">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="70e3a-187">"An Azure subscription is required to create pre-configured solutions.</span><span class="sxs-lookup"><span data-stu-id="70e3a-187">"An Azure subscription is required to create pre-configured solutions.</span></span> <span data-ttu-id="70e3a-188">You can create a free trial account in just a couple of minutes."</span><span class="sxs-lookup"><span data-stu-id="70e3a-188">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="70e3a-189">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span><span class="sxs-lookup"><span data-stu-id="70e3a-189">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span></span> <span data-ttu-id="70e3a-190">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="70e3a-190">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70e3a-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="70e3a-191">Next steps</span></span>
<span data-ttu-id="70e3a-192">To continue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="70e3a-192">To continue learning about IoT Suite, see how you can [customize a preconfigured solution][lnk-customize].</span></span>

[img-flowchart]: media/iot-suite-v1-permissions/flowchart.png

[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]: ../active-directory/active-directory-assign-admin-roles.md
[lnk-portal]: https://portal.azure.com/
[lnk-create-edit-users]: ../active-directory/active-directory-create-users.md
[lnk-assign-app-roles]:../active-directory/manage-apps/assign-user-or-group-access-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin/
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-suite-v1-guidance-on-customizing-preconfigured-solutions.md
