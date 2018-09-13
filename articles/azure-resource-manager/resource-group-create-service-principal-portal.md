---
title: Create identity for Azure app in portal | Microsoft Docs
description: Describes how to create a new Azure Active Directory application and service principal that can be used with the role-based access control in Azure Resource Manager to manage access to resources.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2018
ms.author: tomfitz
ms.openlocfilehash: fc0ccd84f493fd69c84515331386592ec11a887e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803773"
---
# <a name="use-portal-to-create-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="f6af6-103">Use portal to create an Azure Active Directory application and service principal that can access resources</span><span class="sxs-lookup"><span data-stu-id="f6af6-103">Use portal to create an Azure Active Directory application and service principal that can access resources</span></span>

<span data-ttu-id="f6af6-104">When you have code that needs to access or modify resources, you must set up an Azure Active Directory (AD) application.</span><span class="sxs-lookup"><span data-stu-id="f6af6-104">When you have code that needs to access or modify resources, you must set up an Azure Active Directory (AD) application.</span></span> <span data-ttu-id="f6af6-105">You can then assign the required permissions to the AD application.</span><span class="sxs-lookup"><span data-stu-id="f6af6-105">You can then assign the required permissions to the AD application.</span></span> <span data-ttu-id="f6af6-106">This approach is preferable to running the app under your own credentials because you can assign permissions to the app identity that are different than your own permissions.</span><span class="sxs-lookup"><span data-stu-id="f6af6-106">This approach is preferable to running the app under your own credentials because you can assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="f6af6-107">Typically, these permissions are restricted to exactly what the app needs to do.</span><span class="sxs-lookup"><span data-stu-id="f6af6-107">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>

<span data-ttu-id="f6af6-108">This article shows you how to perform these steps through the portal.</span><span class="sxs-lookup"><span data-stu-id="f6af6-108">This article shows you how to perform these steps through the portal.</span></span> <span data-ttu-id="f6af6-109">It focuses on a single-tenant application where the application is intended to run within only one organization.</span><span class="sxs-lookup"><span data-stu-id="f6af6-109">It focuses on a single-tenant application where the application is intended to run within only one organization.</span></span> <span data-ttu-id="f6af6-110">You typically use single-tenant applications for line-of-business applications that run within your organization.</span><span class="sxs-lookup"><span data-stu-id="f6af6-110">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f6af6-111">Instead of creating a service principal, consider using Azure AD Managed Service Identity for your application identity.</span><span class="sxs-lookup"><span data-stu-id="f6af6-111">Instead of creating a service principal, consider using Azure AD Managed Service Identity for your application identity.</span></span> <span data-ttu-id="f6af6-112">Azure AD MSI is a public preview feature of Azure Active Directory that simplifies creating an identity for code.</span><span class="sxs-lookup"><span data-stu-id="f6af6-112">Azure AD MSI is a public preview feature of Azure Active Directory that simplifies creating an identity for code.</span></span> <span data-ttu-id="f6af6-113">If your code runs on a service that supports Azure AD MSI and accesses resources that support Azure Active Directory authentication, Azure AD MSI is a better option for you.</span><span class="sxs-lookup"><span data-stu-id="f6af6-113">If your code runs on a service that supports Azure AD MSI and accesses resources that support Azure Active Directory authentication, Azure AD MSI is a better option for you.</span></span> <span data-ttu-id="f6af6-114">To learn more about Azure AD MSI, including which services currently support it, see [Managed Service Identity for Azure resources](../active-directory/managed-identities-azure-resources/overview.md).</span><span class="sxs-lookup"><span data-stu-id="f6af6-114">To learn more about Azure AD MSI, including which services currently support it, see [Managed Service Identity for Azure resources](../active-directory/managed-identities-azure-resources/overview.md).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="f6af6-115">Required permissions</span><span class="sxs-lookup"><span data-stu-id="f6af6-115">Required permissions</span></span>

<span data-ttu-id="f6af6-116">To complete this article, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f6af6-116">To complete this article, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.</span></span> <span data-ttu-id="f6af6-117">Let's make sure you have the right permissions to perform those steps.</span><span class="sxs-lookup"><span data-stu-id="f6af6-117">Let's make sure you have the right permissions to perform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="f6af6-118">Check Azure Active Directory permissions</span><span class="sxs-lookup"><span data-stu-id="f6af6-118">Check Azure Active Directory permissions</span></span>

1. <span data-ttu-id="f6af6-119">Select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-119">Select **Azure Active Directory**.</span></span>

   ![select azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

1. <span data-ttu-id="f6af6-121">In Azure Active Directory, select **User settings**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-121">In Azure Active Directory, select **User settings**.</span></span>

   ![select user settings](./media/resource-group-create-service-principal-portal/select-user-settings.png)

1. <span data-ttu-id="f6af6-123">Check the **App registrations** setting.</span><span class="sxs-lookup"><span data-stu-id="f6af6-123">Check the **App registrations** setting.</span></span> <span data-ttu-id="f6af6-124">If set to **Yes**, non-admin users can register AD apps.</span><span class="sxs-lookup"><span data-stu-id="f6af6-124">If set to **Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="f6af6-125">This setting means any user in the Azure AD tenant can register an app.</span><span class="sxs-lookup"><span data-stu-id="f6af6-125">This setting means any user in the Azure AD tenant can register an app.</span></span> <span data-ttu-id="f6af6-126">You can proceed to [Check Azure subscription permissions](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="f6af6-126">You can proceed to [Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

   ![view app registrations](./media/resource-group-create-service-principal-portal/view-app-registrations.png)

1. <span data-ttu-id="f6af6-128">If the app registrations setting is set to **No**, only [global administrators](../active-directory/users-groups-roles/directory-assign-admin-roles.md) can register apps.</span><span class="sxs-lookup"><span data-stu-id="f6af6-128">If the app registrations setting is set to **No**, only [global administrators](../active-directory/users-groups-roles/directory-assign-admin-roles.md) can register apps.</span></span> <span data-ttu-id="f6af6-129">Check whether your account is an admin for the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="f6af6-129">Check whether your account is an admin for the Azure AD tenant.</span></span> <span data-ttu-id="f6af6-130">Select **Overview** and look at your user information.</span><span class="sxs-lookup"><span data-stu-id="f6af6-130">Select **Overview** and look at your user information.</span></span> <span data-ttu-id="f6af6-131">If your account is assigned to the User role, but the app registration setting (from the preceding step) is limited to admin users, ask your administrator to either assign you to the global administrator role, or to enable users to register apps.</span><span class="sxs-lookup"><span data-stu-id="f6af6-131">If your account is assigned to the User role, but the app registration setting (from the preceding step) is limited to admin users, ask your administrator to either assign you to the global administrator role, or to enable users to register apps.</span></span>

   ![find user](./media/resource-group-create-service-principal-portal/view-user-info.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="f6af6-133">Check Azure subscription permissions</span><span class="sxs-lookup"><span data-stu-id="f6af6-133">Check Azure subscription permissions</span></span>

<span data-ttu-id="f6af6-134">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access to assign an AD app to a role.</span><span class="sxs-lookup"><span data-stu-id="f6af6-134">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access to assign an AD app to a role.</span></span> <span data-ttu-id="f6af6-135">This action is granted through the [Owner](../role-based-access-control/built-in-roles.md#owner) role or [User Access Administrator](../role-based-access-control/built-in-roles.md#user-access-administrator) role.</span><span class="sxs-lookup"><span data-stu-id="f6af6-135">This action is granted through the [Owner](../role-based-access-control/built-in-roles.md#owner) role or [User Access Administrator](../role-based-access-control/built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="f6af6-136">If your account is assigned to the **Contributor** role, you do not have adequate permission.</span><span class="sxs-lookup"><span data-stu-id="f6af6-136">If your account is assigned to the **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="f6af6-137">You receive an error when attempting to assign the service principal to a role.</span><span class="sxs-lookup"><span data-stu-id="f6af6-137">You receive an error when attempting to assign the service principal to a role.</span></span>

<span data-ttu-id="f6af6-138">To check your subscription permissions:</span><span class="sxs-lookup"><span data-stu-id="f6af6-138">To check your subscription permissions:</span></span>

1. <span data-ttu-id="f6af6-139">Select your account in the upper right corner, and select **My permissions**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-139">Select your account in the upper right corner, and select **My permissions**.</span></span>

   ![select user permissions](./media/resource-group-create-service-principal-portal/select-my-permissions.png)

1. <span data-ttu-id="f6af6-141">From the drop-down list, select the subscription.</span><span class="sxs-lookup"><span data-stu-id="f6af6-141">From the drop-down list, select the subscription.</span></span> <span data-ttu-id="f6af6-142">Select **Click here to view complete access details for this subscription**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-142">Select **Click here to view complete access details for this subscription**.</span></span>

   ![find user](./media/resource-group-create-service-principal-portal/view-details.png)

1. <span data-ttu-id="f6af6-144">View your assigned roles, and determine if you have adequate permissions to assign an AD app to a role.</span><span class="sxs-lookup"><span data-stu-id="f6af6-144">View your assigned roles, and determine if you have adequate permissions to assign an AD app to a role.</span></span> <span data-ttu-id="f6af6-145">If not, ask your subscription administrator to add you to User Access Administrator role.</span><span class="sxs-lookup"><span data-stu-id="f6af6-145">If not, ask your subscription administrator to add you to User Access Administrator role.</span></span> <span data-ttu-id="f6af6-146">In the following image, the user is assigned to the Owner role, which means that user has adequate permissions.</span><span class="sxs-lookup"><span data-stu-id="f6af6-146">In the following image, the user is assigned to the Owner role, which means that user has adequate permissions.</span></span>

   ![show permissions](./media/resource-group-create-service-principal-portal/view-user-role.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="f6af6-148">Create an Azure Active Directory application</span><span class="sxs-lookup"><span data-stu-id="f6af6-148">Create an Azure Active Directory application</span></span>

1. <span data-ttu-id="f6af6-149">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f6af6-149">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
1. <span data-ttu-id="f6af6-150">Select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-150">Select **Azure Active Directory**.</span></span>

   ![select azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

1. <span data-ttu-id="f6af6-152">Select **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-152">Select **App registrations**.</span></span>

   ![select app registrations](./media/resource-group-create-service-principal-portal/select-app-registrations.png)

1. <span data-ttu-id="f6af6-154">Select **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-154">Select **New application registration**.</span></span>

   ![add app](./media/resource-group-create-service-principal-portal/select-add-app.png)

1. <span data-ttu-id="f6af6-156">Provide a name and URL for the application.</span><span class="sxs-lookup"><span data-stu-id="f6af6-156">Provide a name and URL for the application.</span></span> <span data-ttu-id="f6af6-157">Select **Web app / API** for the type of application you want to create.</span><span class="sxs-lookup"><span data-stu-id="f6af6-157">Select **Web app / API** for the type of application you want to create.</span></span> <span data-ttu-id="f6af6-158">You cannot create credentials for a [Native application](../active-directory/manage-apps/application-proxy-configure-native-client-application.md); therefore, that type does not work for an automated application.</span><span class="sxs-lookup"><span data-stu-id="f6af6-158">You cannot create credentials for a [Native application](../active-directory/manage-apps/application-proxy-configure-native-client-application.md); therefore, that type does not work for an automated application.</span></span> <span data-ttu-id="f6af6-159">After setting the values, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-159">After setting the values, select **Create**.</span></span>

   ![name application](./media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="f6af6-161">You have created your application.</span><span class="sxs-lookup"><span data-stu-id="f6af6-161">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="f6af6-162">Get application ID and authentication key</span><span class="sxs-lookup"><span data-stu-id="f6af6-162">Get application ID and authentication key</span></span>

<span data-ttu-id="f6af6-163">When programmatically logging in, you need the ID for your application and an authentication key.</span><span class="sxs-lookup"><span data-stu-id="f6af6-163">When programmatically logging in, you need the ID for your application and an authentication key.</span></span> <span data-ttu-id="f6af6-164">To get those values, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="f6af6-164">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="f6af6-165">From **App registrations** in Azure Active Directory, select your application.</span><span class="sxs-lookup"><span data-stu-id="f6af6-165">From **App registrations** in Azure Active Directory, select your application.</span></span>

   ![select application](./media/resource-group-create-service-principal-portal/select-app.png)

1. <span data-ttu-id="f6af6-167">Copy the **Application ID** and store it in your application code.</span><span class="sxs-lookup"><span data-stu-id="f6af6-167">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="f6af6-168">Some [sample applications](#log-in-as-the-application) refer to this value as the client ID.</span><span class="sxs-lookup"><span data-stu-id="f6af6-168">Some [sample applications](#log-in-as-the-application) refer to this value as the client ID.</span></span>

   ![client ID](./media/resource-group-create-service-principal-portal/copy-app-id.png)

1. <span data-ttu-id="f6af6-170">To generate an authentication key, select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-170">To generate an authentication key, select **Settings**.</span></span>

   ![select settings](./media/resource-group-create-service-principal-portal/select-settings.png)

1. <span data-ttu-id="f6af6-172">To generate an authentication key, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-172">To generate an authentication key, select **Keys**.</span></span>

   ![select keys](./media/resource-group-create-service-principal-portal/select-keys.png)

1. <span data-ttu-id="f6af6-174">Provide a description of the key, and a duration for the key.</span><span class="sxs-lookup"><span data-stu-id="f6af6-174">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="f6af6-175">When done, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-175">When done, select **Save**.</span></span>

   ![save key](./media/resource-group-create-service-principal-portal/save-key.png)

   <span data-ttu-id="f6af6-177">After saving the key, the value of the key is displayed.</span><span class="sxs-lookup"><span data-stu-id="f6af6-177">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="f6af6-178">Copy this value because you are not able to retrieve the key later.</span><span class="sxs-lookup"><span data-stu-id="f6af6-178">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="f6af6-179">You provide the key value with the application ID to log in as the application.</span><span class="sxs-lookup"><span data-stu-id="f6af6-179">You provide the key value with the application ID to log in as the application.</span></span> <span data-ttu-id="f6af6-180">Store the key value where your application can retrieve it.</span><span class="sxs-lookup"><span data-stu-id="f6af6-180">Store the key value where your application can retrieve it.</span></span>

   ![saved key](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="f6af6-182">Get tenant ID</span><span class="sxs-lookup"><span data-stu-id="f6af6-182">Get tenant ID</span></span>

<span data-ttu-id="f6af6-183">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span><span class="sxs-lookup"><span data-stu-id="f6af6-183">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span></span>

1. <span data-ttu-id="f6af6-184">Select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-184">Select **Azure Active Directory**.</span></span>

   ![select azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

1. <span data-ttu-id="f6af6-186">To get the tenant ID, select **Properties** for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="f6af6-186">To get the tenant ID, select **Properties** for your Azure AD tenant.</span></span>

   ![select Azure AD properties](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

1. <span data-ttu-id="f6af6-188">Copy the **Directory ID**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-188">Copy the **Directory ID**.</span></span> <span data-ttu-id="f6af6-189">This value is your tenant ID.</span><span class="sxs-lookup"><span data-stu-id="f6af6-189">This value is your tenant ID.</span></span>

   ![tenant ID](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-to-role"></a><span data-ttu-id="f6af6-191">Assign application to role</span><span class="sxs-lookup"><span data-stu-id="f6af6-191">Assign application to role</span></span>

<span data-ttu-id="f6af6-192">To access resources in your subscription, you must assign the application to a role.</span><span class="sxs-lookup"><span data-stu-id="f6af6-192">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="f6af6-193">Decide which role represents the right permissions for the application.</span><span class="sxs-lookup"><span data-stu-id="f6af6-193">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="f6af6-194">To learn about the available roles, see [RBAC: Built in Roles](../role-based-access-control/built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="f6af6-194">To learn about the available roles, see [RBAC: Built in Roles](../role-based-access-control/built-in-roles.md).</span></span>

<span data-ttu-id="f6af6-195">You can set the scope at the level of the subscription, resource group, or resource.</span><span class="sxs-lookup"><span data-stu-id="f6af6-195">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="f6af6-196">Permissions are inherited to lower levels of scope.</span><span class="sxs-lookup"><span data-stu-id="f6af6-196">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="f6af6-197">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span><span class="sxs-lookup"><span data-stu-id="f6af6-197">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="f6af6-198">Navigate to the level of scope you wish to assign the application to.</span><span class="sxs-lookup"><span data-stu-id="f6af6-198">Navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="f6af6-199">For example, to assign a role at the subscription scope, select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-199">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="f6af6-200">You could instead select a resource group or resource.</span><span class="sxs-lookup"><span data-stu-id="f6af6-200">You could instead select a resource group or resource.</span></span>

   ![select subscription](./media/resource-group-create-service-principal-portal/select-subscription.png)

1. <span data-ttu-id="f6af6-202">Select the particular subscription (resource group or resource) to assign the application to.</span><span class="sxs-lookup"><span data-stu-id="f6af6-202">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

   ![select subscription for assignment](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

1. <span data-ttu-id="f6af6-204">Select **Access Control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-204">Select **Access Control (IAM)**.</span></span>

   ![select access](./media/resource-group-create-service-principal-portal/select-access-control.png)

1. <span data-ttu-id="f6af6-206">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-206">Select **Add**.</span></span>

   ![select add](./media/resource-group-create-service-principal-portal/select-add.png)

1. <span data-ttu-id="f6af6-208">Select the role you wish to assign to the application.</span><span class="sxs-lookup"><span data-stu-id="f6af6-208">Select the role you wish to assign to the application.</span></span> <span data-ttu-id="f6af6-209">In order to allow the application execute actions like **reboot**, **start** and **stop** instances, you must have to select the role **Contributor**.</span><span class="sxs-lookup"><span data-stu-id="f6af6-209">In order to allow the application execute actions like **reboot**, **start** and **stop** instances, you must have to select the role **Contributor**.</span></span> <span data-ttu-id="f6af6-210">The following image shows the **Reader** role.</span><span class="sxs-lookup"><span data-stu-id="f6af6-210">The following image shows the **Reader** role.</span></span>

   ![select role](./media/resource-group-create-service-principal-portal/select-role.png)

1. <span data-ttu-id="f6af6-212">By default, Azure Active Directory applications aren't displayed in the available options.</span><span class="sxs-lookup"><span data-stu-id="f6af6-212">By default, Azure Active Directory applications aren't displayed in the available options.</span></span> <span data-ttu-id="f6af6-213">To find your application, you must provide the name of it in the search field.</span><span class="sxs-lookup"><span data-stu-id="f6af6-213">To find your application, you must provide the name of it in the search field.</span></span> <span data-ttu-id="f6af6-214">Select it.</span><span class="sxs-lookup"><span data-stu-id="f6af6-214">Select it.</span></span>

   ![search for app](./media/resource-group-create-service-principal-portal/search-app.png)

1. <span data-ttu-id="f6af6-216">Select **Save** to finish assigning the role.</span><span class="sxs-lookup"><span data-stu-id="f6af6-216">Select **Save** to finish assigning the role.</span></span> <span data-ttu-id="f6af6-217">You see your application in the list of users assigned to a role for that scope.</span><span class="sxs-lookup"><span data-stu-id="f6af6-217">You see your application in the list of users assigned to a role for that scope.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6af6-218">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6af6-218">Next steps</span></span>
* <span data-ttu-id="f6af6-219">To set up a multi-tenant application, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="f6af6-219">To set up a multi-tenant application, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="f6af6-220">To learn about specifying security policies, see [Azure Role-based Access Control](../role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f6af6-220">To learn about specifying security policies, see [Azure Role-based Access Control](../role-based-access-control/role-assignments-portal.md).</span></span>  
* <span data-ttu-id="f6af6-221">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../role-based-access-control/resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="f6af6-221">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../role-based-access-control/resource-provider-operations.md).</span></span>
