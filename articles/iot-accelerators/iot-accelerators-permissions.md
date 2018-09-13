---
title: Azure IoT solution accelerators and Azure Active Directory | Microsoft Docs
description: Describes how Azure IoT solution accelerators uses Azure Active Directory to manage permissions.
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 11/10/2017
ms.author: dobett
ms.openlocfilehash: c88ae933360b5040ad3d2b877041049512f08b0d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871735"
---
# <a name="permissions-on-the-azureiotsolutionscom-site"></a><span data-ttu-id="3c24f-103">Permissions on the azureiotsolutions.com site</span><span class="sxs-lookup"><span data-stu-id="3c24f-103">Permissions on the azureiotsolutions.com site</span></span>

## <a name="what-happens-when-you-sign-in"></a><span data-ttu-id="3c24f-104">What happens when you sign in</span><span class="sxs-lookup"><span data-stu-id="3c24f-104">What happens when you sign in</span></span>

<span data-ttu-id="3c24f-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsolutions], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3c24f-105">The first time you sign in at [azureiotsuite.com][lnk-azureiotsolutions], the site determines the permission levels you have based on the currently selected Azure Active Directory (AAD) tenant and Azure subscription.</span></span>

1. <span data-ttu-id="3c24f-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span><span class="sxs-lookup"><span data-stu-id="3c24f-106">First, to populate the list of tenants seen next to your username, the site finds out from Azure which AAD tenants you belong to.</span></span> <span data-ttu-id="3c24f-107">Currently, the site can only obtain user tokens for one tenant at a time.</span><span class="sxs-lookup"><span data-stu-id="3c24f-107">Currently, the site can only obtain user tokens for one tenant at a time.</span></span> <span data-ttu-id="3c24f-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span><span class="sxs-lookup"><span data-stu-id="3c24f-108">Therefore, when you switch tenants using the dropdown in the top right corner, the site logs you in to that tenant to obtain the tokens for that tenant.</span></span>

2. <span data-ttu-id="3c24f-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span><span class="sxs-lookup"><span data-stu-id="3c24f-109">Next, the site finds out from Azure which subscriptions you have associated with the selected tenant.</span></span> <span data-ttu-id="3c24f-110">You see the available subscriptions when you create a new solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="3c24f-110">You see the available subscriptions when you create a new solution accelerator.</span></span>

3. <span data-ttu-id="3c24f-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as solution accelerators and populates the tiles on the home page.</span><span class="sxs-lookup"><span data-stu-id="3c24f-111">Finally, the site retrieves all the resources in the subscriptions and resource groups tagged as solution accelerators and populates the tiles on the home page.</span></span>

<span data-ttu-id="3c24f-112">The following sections describe the roles that control access to the solution accelerators.</span><span class="sxs-lookup"><span data-stu-id="3c24f-112">The following sections describe the roles that control access to the solution accelerators.</span></span>

## <a name="aad-roles"></a><span data-ttu-id="3c24f-113">AAD roles</span><span class="sxs-lookup"><span data-stu-id="3c24f-113">AAD roles</span></span>

<span data-ttu-id="3c24f-114">The AAD roles control the ability to provision solution accelerators, to manage users and some Azure services in a solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="3c24f-114">The AAD roles control the ability to provision solution accelerators, to manage users and some Azure services in a solution accelerator.</span></span>

<span data-ttu-id="3c24f-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span><span class="sxs-lookup"><span data-stu-id="3c24f-115">You can find more information about administrator roles in AAD in [Assigning administrator roles in Azure AD][lnk-aad-admin].</span></span> <span data-ttu-id="3c24f-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the solution accelerators.</span><span class="sxs-lookup"><span data-stu-id="3c24f-116">The current article focuses on the **Global Administrator** and the **User** directory roles as used by the solution accelerators.</span></span>

### <a name="global-administrator"></a><span data-ttu-id="3c24f-117">Global administrator</span><span class="sxs-lookup"><span data-stu-id="3c24f-117">Global administrator</span></span>

<span data-ttu-id="3c24f-118">There can be many global administrators per AAD tenant:</span><span class="sxs-lookup"><span data-stu-id="3c24f-118">There can be many global administrators per AAD tenant:</span></span>

* <span data-ttu-id="3c24f-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span><span class="sxs-lookup"><span data-stu-id="3c24f-119">When you create an AAD tenant, you are by default the global administrator of that tenant.</span></span>
* <span data-ttu-id="3c24f-120">The global administrator can provision a basic and standard solution accelerators (a basic deployment uses a single Azure Virtual Machine).</span><span class="sxs-lookup"><span data-stu-id="3c24f-120">The global administrator can provision a basic and standard solution accelerators (a basic deployment uses a single Azure Virtual Machine).</span></span>

### <a name="domain-user"></a><span data-ttu-id="3c24f-121">Domain user</span><span class="sxs-lookup"><span data-stu-id="3c24f-121">Domain user</span></span>

<span data-ttu-id="3c24f-122">There can be many domain users per AAD tenant:</span><span class="sxs-lookup"><span data-stu-id="3c24f-122">There can be many domain users per AAD tenant:</span></span>

* <span data-ttu-id="3c24f-123">A domain user can provision a basic solution accelerator through the [azureiotsolutions.com][lnk-azureiotsolutions] site.</span><span class="sxs-lookup"><span data-stu-id="3c24f-123">A domain user can provision a basic solution accelerator through the [azureiotsolutions.com][lnk-azureiotsolutions] site.</span></span>
* <span data-ttu-id="3c24f-124">A domain user can create a basic solution accelerator using the CLI.</span><span class="sxs-lookup"><span data-stu-id="3c24f-124">A domain user can create a basic solution accelerator using the CLI.</span></span>

### <a name="guest-user"></a><span data-ttu-id="3c24f-125">Guest User</span><span class="sxs-lookup"><span data-stu-id="3c24f-125">Guest User</span></span>

<span data-ttu-id="3c24f-126">There can be many guest users per AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="3c24f-126">There can be many guest users per AAD tenant.</span></span> <span data-ttu-id="3c24f-127">Guest users have a limited set of rights in the AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="3c24f-127">Guest users have a limited set of rights in the AAD tenant.</span></span> <span data-ttu-id="3c24f-128">As a result, guest users cannot provision a solution accelerator in the AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="3c24f-128">As a result, guest users cannot provision a solution accelerator in the AAD tenant.</span></span>

<span data-ttu-id="3c24f-129">For more information about users and roles in AAD, see the following resources:</span><span class="sxs-lookup"><span data-stu-id="3c24f-129">For more information about users and roles in AAD, see the following resources:</span></span>

* <span data-ttu-id="3c24f-130">[Create users in Azure AD][lnk-create-edit-users]</span><span class="sxs-lookup"><span data-stu-id="3c24f-130">[Create users in Azure AD][lnk-create-edit-users]</span></span>
* <span data-ttu-id="3c24f-131">[Assign users to apps][lnk-assign-app-roles]</span><span class="sxs-lookup"><span data-stu-id="3c24f-131">[Assign users to apps][lnk-assign-app-roles]</span></span>

## <a name="azure-subscription-administrator-roles"></a><span data-ttu-id="3c24f-132">Azure subscription administrator roles</span><span class="sxs-lookup"><span data-stu-id="3c24f-132">Azure subscription administrator roles</span></span>

<span data-ttu-id="3c24f-133">The Azure admin roles control the ability to map an Azure subscription to an AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="3c24f-133">The Azure admin roles control the ability to map an Azure subscription to an AAD tenant.</span></span>

<span data-ttu-id="3c24f-134">Find out more about the Azure admin roles in the article [Add or change Azure subscription administrators][lnk-admin-roles].</span><span class="sxs-lookup"><span data-stu-id="3c24f-134">Find out more about the Azure admin roles in the article [Add or change Azure subscription administrators][lnk-admin-roles].</span></span>

## <a name="faq"></a><span data-ttu-id="3c24f-135">FAQ</span><span class="sxs-lookup"><span data-stu-id="3c24f-135">FAQ</span></span>

### <a name="im-a-service-administrator-and-id-like-to-change-the-directory-mapping-between-my-subscription-and-a-specific-aad-tenant-how-do-i-complete-this-task"></a><span data-ttu-id="3c24f-136">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="3c24f-136">I'm a service administrator and I'd like to change the directory mapping between my subscription and a specific AAD tenant.</span></span> <span data-ttu-id="3c24f-137">How do I complete this task?</span><span class="sxs-lookup"><span data-stu-id="3c24f-137">How do I complete this task?</span></span>

<span data-ttu-id="3c24f-138">See [To add an existing subscription to your Azure AD directory](../active-directory/fundamentals/active-directory-how-subscriptions-associated-directory.md#to-associate-an-existing-subscription-to-your-azure-ad-directory)</span><span class="sxs-lookup"><span data-stu-id="3c24f-138">See [To add an existing subscription to your Azure AD directory](../active-directory/fundamentals/active-directory-how-subscriptions-associated-directory.md#to-associate-an-existing-subscription-to-your-azure-ad-directory)</span></span>

### <a name="i-want-to-change-a-service-administrator-or-co-administrator-when-logged-in-with-an-organizational-account"></a><span data-ttu-id="3c24f-139">I want to change a Service Administrator or Co-Administrator when logged in with an organizational account</span><span class="sxs-lookup"><span data-stu-id="3c24f-139">I want to change a Service Administrator or Co-Administrator when logged in with an organizational account</span></span>

<span data-ttu-id="3c24f-140">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organizational account][lnk-service-admins].</span><span class="sxs-lookup"><span data-stu-id="3c24f-140">See the support article [Changing Service Administrator and Co-Administrator when logged in with an organizational account][lnk-service-admins].</span></span>

### <a name="why-am-i-seeing-this-error-your-account-does-not-have-the-proper-permissions-to-create-a-solution-please-check-with-your-account-administrator-or-try-with-a-different-account"></a><span data-ttu-id="3c24f-141">Why am I seeing this error?</span><span class="sxs-lookup"><span data-stu-id="3c24f-141">Why am I seeing this error?</span></span> <span data-ttu-id="3c24f-142">"Your account does not have the proper permissions to create a solution.</span><span class="sxs-lookup"><span data-stu-id="3c24f-142">"Your account does not have the proper permissions to create a solution.</span></span> <span data-ttu-id="3c24f-143">Please check with your account administrator or try with a different account."</span><span class="sxs-lookup"><span data-stu-id="3c24f-143">Please check with your account administrator or try with a different account."</span></span>

<span data-ttu-id="3c24f-144">Look at the following diagram for guidance:</span><span class="sxs-lookup"><span data-stu-id="3c24f-144">Look at the following diagram for guidance:</span></span>

![][img-flowchart]

> [!NOTE]
> <span data-ttu-id="3c24f-145">If you continue to see the error after validating you are a global administrator of the AAD tenant and a co-administrator of the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span><span class="sxs-lookup"><span data-stu-id="3c24f-145">If you continue to see the error after validating you are a global administrator of the AAD tenant and a co-administrator of the subscription, have your account administrator remove the user and reassign necessary permissions in this order.</span></span> <span data-ttu-id="3c24f-146">First, add the user as a global administrator and then add user as a co-administrator of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3c24f-146">First, add the user as a global administrator and then add user as a co-administrator of the Azure subscription.</span></span> <span data-ttu-id="3c24f-147">If issues persist, contact [Help & Support][lnk-help-support].</span><span class="sxs-lookup"><span data-stu-id="3c24f-147">If issues persist, contact [Help & Support][lnk-help-support].</span></span>

### <a name="why-am-i-seeing-this-error-when-i-have-an-azure-subscription-an-azure-subscription-is-required-to-create-pre-configured-solutions-you-can-create-a-free-trial-account-in-just-a-couple-of-minutes"></a><span data-ttu-id="3c24f-148">Why am I seeing this error when I have an Azure subscription?</span><span class="sxs-lookup"><span data-stu-id="3c24f-148">Why am I seeing this error when I have an Azure subscription?</span></span> <span data-ttu-id="3c24f-149">"An Azure subscription is required to create pre-configured solutions.</span><span class="sxs-lookup"><span data-stu-id="3c24f-149">"An Azure subscription is required to create pre-configured solutions.</span></span> <span data-ttu-id="3c24f-150">You can create a free trial account in just a couple of minutes."</span><span class="sxs-lookup"><span data-stu-id="3c24f-150">You can create a free trial account in just a couple of minutes."</span></span>

<span data-ttu-id="3c24f-151">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span><span class="sxs-lookup"><span data-stu-id="3c24f-151">If you're certain you have an Azure subscription, validate the tenant mapping for your subscription and ensure the correct tenant is selected in the dropdown.</span></span> <span data-ttu-id="3c24f-152">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span><span class="sxs-lookup"><span data-stu-id="3c24f-152">If you’ve validated the desired tenant is correct, follow the preceding diagram and validate the mapping of your subscription and this AAD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c24f-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c24f-153">Next steps</span></span>
<span data-ttu-id="3c24f-154">To continue learning about IoT solution accelerators, see how you can [customize a solution accelerator][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="3c24f-154">To continue learning about IoT solution accelerators, see how you can [customize a solution accelerator][lnk-customize].</span></span>

[img-flowchart]: media/iot-accelerators-permissions/flowchart.png

[lnk-azureiotsolutions]: https://www.azureiotsolutions.com
[lnk-rm-github-repo]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-pm-github-repo]: https://github.com/Azure/azure-iot-predictive-maintenance
[lnk-cf-github-repo]: https://github.com/Azure/azure-iot-connected-factory
[lnk-aad-admin]:../active-directory/users-groups-roles/directory-assign-admin-roles.md
[lnk-portal]: https://portal.azure.com
[lnk-create-edit-users]:../active-directory/fundamentals/active-directory-users-profile-azure-portal.md
[lnk-assign-app-roles]:../active-directory/manage-apps/assign-user-or-group-access-portal.md
[lnk-service-admins]: https://azure.microsoft.com/support/changing-service-admin-and-co-admin
[lnk-admin-roles]: ../billing/billing-add-change-azure-subscription-administrator.md
[lnk-resource-cs]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/DeviceAdministration/Web/Security/RolePermissions.cs
[lnk-help-support]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[lnk-customize]: iot-accelerators-remote-monitoring-customize.md
