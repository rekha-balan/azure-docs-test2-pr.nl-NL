---
title: Create identity for Azure app in portal | Microsoft Docs
description: Describes how to create a new Azure Active Directory application and service principal that can be used with the role-based access control in Azure Resource Manager to manage access to resources.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/17/2017
ms.author: tomfitz
ms.openlocfilehash: a0c0c931ed0cfe03d98d9b1162f0c99ec4b5e96d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562933"
---
# <a name="use-portal-to-create-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a><span data-ttu-id="e63fe-103">Use portal to create an Azure Active Directory application and service principal that can access resources</span><span class="sxs-lookup"><span data-stu-id="e63fe-103">Use portal to create an Azure Active Directory application and service principal that can access resources</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-authenticate-service-principal.md)
> * [Azure CLI](resource-group-authenticate-service-principal-cli.md)
> * [Portal](resource-group-create-service-principal-portal.md)
>
>

<span data-ttu-id="e63fe-107">When you have an application that needs to access or modify resources, you must set up an Azure Active Directory (AD) application and assign the required permissions to it.</span><span class="sxs-lookup"><span data-stu-id="e63fe-107">When you have an application that needs to access or modify resources, you must set up an Azure Active Directory (AD) application and assign the required permissions to it.</span></span> <span data-ttu-id="e63fe-108">This approach is preferable to running the app under your own credentials because:</span><span class="sxs-lookup"><span data-stu-id="e63fe-108">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="e63fe-109">You can assign permissions to the app identity that are different than your own permissions.</span><span class="sxs-lookup"><span data-stu-id="e63fe-109">You can assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="e63fe-110">Typically, these permissions are restricted to exactly what the app needs to do.</span><span class="sxs-lookup"><span data-stu-id="e63fe-110">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="e63fe-111">You do not have to change the app's credentials if your responsibilities change.</span><span class="sxs-lookup"><span data-stu-id="e63fe-111">You do not have to change the app's credentials if your responsibilities change.</span></span> 
* <span data-ttu-id="e63fe-112">You can use a certificate to automate authentication when executing an unattended script.</span><span class="sxs-lookup"><span data-stu-id="e63fe-112">You can use a certificate to automate authentication when executing an unattended script.</span></span>

<span data-ttu-id="e63fe-113">This topic shows you how to perform those steps through the portal.</span><span class="sxs-lookup"><span data-stu-id="e63fe-113">This topic shows you how to perform those steps through the portal.</span></span> <span data-ttu-id="e63fe-114">It focuses on a single-tenant application where the application is intended to run within only one organization.</span><span class="sxs-lookup"><span data-stu-id="e63fe-114">It focuses on a single-tenant application where the application is intended to run within only one organization.</span></span> <span data-ttu-id="e63fe-115">You typically use single-tenant applications for line-of-business applications that run within your organization.</span><span class="sxs-lookup"><span data-stu-id="e63fe-115">You typically use single-tenant applications for line-of-business applications that run within your organization.</span></span>
 
## <a name="required-permissions"></a><span data-ttu-id="e63fe-116">Required permissions</span><span class="sxs-lookup"><span data-stu-id="e63fe-116">Required permissions</span></span>
<span data-ttu-id="e63fe-117">To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e63fe-117">To complete this topic, you must have sufficient permissions to register an application with your Azure AD tenant, and assign the application to a role in your Azure subscription.</span></span> <span data-ttu-id="e63fe-118">Let's make sure you have the right permissions to perform those steps.</span><span class="sxs-lookup"><span data-stu-id="e63fe-118">Let's make sure you have the right permissions to perform those steps.</span></span>

### <a name="check-azure-active-directory-permissions"></a><span data-ttu-id="e63fe-119">Check Azure Active Directory permissions</span><span class="sxs-lookup"><span data-stu-id="e63fe-119">Check Azure Active Directory permissions</span></span>
1. <span data-ttu-id="e63fe-120">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e63fe-120">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e63fe-121">Select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-121">Select **Azure Active Directory**.</span></span>

     ![select azure active directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-active-directory.png)
3. <span data-ttu-id="e63fe-123">In Azure Active Directory, select **User settings**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-123">In Azure Active Directory, select **User settings**.</span></span>

     ![select user settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-user-settings.png)
4. <span data-ttu-id="e63fe-125">Check the **App registrations** setting.</span><span class="sxs-lookup"><span data-stu-id="e63fe-125">Check the **App registrations** setting.</span></span> <span data-ttu-id="e63fe-126">If set to **Yes**, non-admin users can register AD apps.</span><span class="sxs-lookup"><span data-stu-id="e63fe-126">If set to **Yes**, non-admin users can register AD apps.</span></span> <span data-ttu-id="e63fe-127">This setting means any user in the Azure AD tenant can register an app.</span><span class="sxs-lookup"><span data-stu-id="e63fe-127">This setting means any user in the Azure AD tenant can register an app.</span></span> <span data-ttu-id="e63fe-128">You can proceed to [Check Azure subscription permissions](#check-azure-subscription-permissions).</span><span class="sxs-lookup"><span data-stu-id="e63fe-128">You can proceed to [Check Azure subscription permissions](#check-azure-subscription-permissions).</span></span>

     ![view app registrations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. <span data-ttu-id="e63fe-130">If the app registrations setting is set to **No**, only admin users can register apps.</span><span class="sxs-lookup"><span data-stu-id="e63fe-130">If the app registrations setting is set to **No**, only admin users can register apps.</span></span> <span data-ttu-id="e63fe-131">You need to check whether your account is an admin for the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="e63fe-131">You need to check whether your account is an admin for the Azure AD tenant.</span></span> <span data-ttu-id="e63fe-132">Select **Overview** and **Find a user** from Quick tasks.</span><span class="sxs-lookup"><span data-stu-id="e63fe-132">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![find user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/find-user.png)
6. <span data-ttu-id="e63fe-134">Search for your account, and select it when you find it.</span><span class="sxs-lookup"><span data-stu-id="e63fe-134">Search for your account, and select it when you find it.</span></span>

     ![search user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/show-user.png)
7. <span data-ttu-id="e63fe-136">For your account, select **Directory role**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-136">For your account, select **Directory role**.</span></span> 

     ![directory role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-directory-role.png)
8. <span data-ttu-id="e63fe-138">View your assigned directory role in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e63fe-138">View your assigned directory role in Azure AD.</span></span> <span data-ttu-id="e63fe-139">If your account is assigned to the User role, but the app registration setting (from the preceding steps) is limited to admin users, ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span><span class="sxs-lookup"><span data-stu-id="e63fe-139">If your account is assigned to the User role, but the app registration setting (from the preceding steps) is limited to admin users, ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

     ![view role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a><span data-ttu-id="e63fe-141">Check Azure subscription permissions</span><span class="sxs-lookup"><span data-stu-id="e63fe-141">Check Azure subscription permissions</span></span>
<span data-ttu-id="e63fe-142">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access to assign an AD app to a role.</span><span class="sxs-lookup"><span data-stu-id="e63fe-142">In your Azure subscription, your account must have `Microsoft.Authorization/*/Write` access to assign an AD app to a role.</span></span> <span data-ttu-id="e63fe-143">This action is granted through the [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span><span class="sxs-lookup"><span data-stu-id="e63fe-143">This action is granted through the [Owner](../active-directory/role-based-access-built-in-roles.md#owner) role or [User Access Administrator](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) role.</span></span> <span data-ttu-id="e63fe-144">If your account is assigned to the **Contributor** role, you do not have adequate permission.</span><span class="sxs-lookup"><span data-stu-id="e63fe-144">If your account is assigned to the **Contributor** role, you do not have adequate permission.</span></span> <span data-ttu-id="e63fe-145">You will receive an error when attempting to assign the service principal to a role.</span><span class="sxs-lookup"><span data-stu-id="e63fe-145">You will receive an error when attempting to assign the service principal to a role.</span></span> 

<span data-ttu-id="e63fe-146">To check your subscription permissions:</span><span class="sxs-lookup"><span data-stu-id="e63fe-146">To check your subscription permissions:</span></span>

1. <span data-ttu-id="e63fe-147">If you are not already looking at your Azure AD account from the preceding steps, select **Azure Active Directory** from the left pane.</span><span class="sxs-lookup"><span data-stu-id="e63fe-147">If you are not already looking at your Azure AD account from the preceding steps, select **Azure Active Directory** from the left pane.</span></span>

2. <span data-ttu-id="e63fe-148">Find your Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="e63fe-148">Find your Azure AD account.</span></span> <span data-ttu-id="e63fe-149">Select **Overview** and **Find a user** from Quick tasks.</span><span class="sxs-lookup"><span data-stu-id="e63fe-149">Select **Overview** and **Find a user** from Quick tasks.</span></span>

     ![find user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/find-user.png)
2. <span data-ttu-id="e63fe-151">Search for your account, and select it when you find it.</span><span class="sxs-lookup"><span data-stu-id="e63fe-151">Search for your account, and select it when you find it.</span></span>

     ![search user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/show-user.png) 
     
3. <span data-ttu-id="e63fe-153">Select **Azure resources**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-153">Select **Azure resources**.</span></span>

     ![select resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. <span data-ttu-id="e63fe-155">View your assigned roles, and determine if you have adequate permissions to assign an AD app to a role.</span><span class="sxs-lookup"><span data-stu-id="e63fe-155">View your assigned roles, and determine if you have adequate permissions to assign an AD app to a role.</span></span> <span data-ttu-id="e63fe-156">If not, ask your subscription administrator to add you to User Access Administrator role.</span><span class="sxs-lookup"><span data-stu-id="e63fe-156">If not, ask your subscription administrator to add you to User Access Administrator role.</span></span> <span data-ttu-id="e63fe-157">In the following image, the user is assigned to the Owner role for two subscriptions, which means that user has adequate permissions.</span><span class="sxs-lookup"><span data-stu-id="e63fe-157">In the following image, the user is assigned to the Owner role for two subscriptions, which means that user has adequate permissions.</span></span> 

     ![show permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a><span data-ttu-id="e63fe-159">Create an Azure Active Directory application</span><span class="sxs-lookup"><span data-stu-id="e63fe-159">Create an Azure Active Directory application</span></span>
1. <span data-ttu-id="e63fe-160">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e63fe-160">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e63fe-161">Select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-161">Select **Azure Active Directory**.</span></span>

     ![select azure active directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-active-directory.png)

4. <span data-ttu-id="e63fe-163">Select **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-163">Select **App registrations**.</span></span>   

     ![select app registrations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. <span data-ttu-id="e63fe-165">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-165">Select **Add**.</span></span>

     ![add app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-add-app.png)

6. <span data-ttu-id="e63fe-167">Provide a name and URL for the application.</span><span class="sxs-lookup"><span data-stu-id="e63fe-167">Provide a name and URL for the application.</span></span> <span data-ttu-id="e63fe-168">Select either **Web app / API** or **Native** for the type of application you want to create.</span><span class="sxs-lookup"><span data-stu-id="e63fe-168">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="e63fe-169">After setting the values, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-169">After setting the values, select **Create**.</span></span>

     ![name application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/create-app.png)

<span data-ttu-id="e63fe-171">You have created your application.</span><span class="sxs-lookup"><span data-stu-id="e63fe-171">You have created your application.</span></span>

## <a name="get-application-id-and-authentication-key"></a><span data-ttu-id="e63fe-172">Get application ID and authentication key</span><span class="sxs-lookup"><span data-stu-id="e63fe-172">Get application ID and authentication key</span></span>
<span data-ttu-id="e63fe-173">When programmatically logging in, you need the ID for your application and an authentication key.</span><span class="sxs-lookup"><span data-stu-id="e63fe-173">When programmatically logging in, you need the ID for your application and an authentication key.</span></span> <span data-ttu-id="e63fe-174">To get those values, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="e63fe-174">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="e63fe-175">From **App registrations** in Azure Active Directory, select your application.</span><span class="sxs-lookup"><span data-stu-id="e63fe-175">From **App registrations** in Azure Active Directory, select your application.</span></span>

     ![select application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-app.png)
2. <span data-ttu-id="e63fe-177">Copy the **Application ID** and store it in your application code.</span><span class="sxs-lookup"><span data-stu-id="e63fe-177">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="e63fe-178">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span><span class="sxs-lookup"><span data-stu-id="e63fe-178">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span></span>

     ![client id](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/copy-app-id.png)
3. <span data-ttu-id="e63fe-180">To generate an authentication key, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-180">To generate an authentication key, select **Keys**.</span></span>

     ![select keys](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-keys.png)
4. <span data-ttu-id="e63fe-182">Provide a description of the key, and a duration for the key.</span><span class="sxs-lookup"><span data-stu-id="e63fe-182">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="e63fe-183">When done, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-183">When done, select **Save**.</span></span>

     ![save key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/save-key.png)

     <span data-ttu-id="e63fe-185">After saving the key, the value of the key is displayed.</span><span class="sxs-lookup"><span data-stu-id="e63fe-185">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="e63fe-186">Copy this value because you are not able to retrieve the key later.</span><span class="sxs-lookup"><span data-stu-id="e63fe-186">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="e63fe-187">You provide the key value with the application ID to log in as the application.</span><span class="sxs-lookup"><span data-stu-id="e63fe-187">You provide the key value with the application ID to log in as the application.</span></span> <span data-ttu-id="e63fe-188">Store the key value where your application can retrieve it.</span><span class="sxs-lookup"><span data-stu-id="e63fe-188">Store the key value where your application can retrieve it.</span></span>

     ![saved key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a><span data-ttu-id="e63fe-190">Get tenant ID</span><span class="sxs-lookup"><span data-stu-id="e63fe-190">Get tenant ID</span></span>
<span data-ttu-id="e63fe-191">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span><span class="sxs-lookup"><span data-stu-id="e63fe-191">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span></span> 

1. <span data-ttu-id="e63fe-192">To get the tenant ID, select **Properties** for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="e63fe-192">To get the tenant ID, select **Properties** for your Azure AD tenant.</span></span> 

     ![select Azure AD properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. <span data-ttu-id="e63fe-194">Copy the **Directory ID**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-194">Copy the **Directory ID**.</span></span> <span data-ttu-id="e63fe-195">This value is your tenant ID.</span><span class="sxs-lookup"><span data-stu-id="e63fe-195">This value is your tenant ID.</span></span>

     ![tenant id](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-to-role"></a><span data-ttu-id="e63fe-197">Assign application to role</span><span class="sxs-lookup"><span data-stu-id="e63fe-197">Assign application to role</span></span>
<span data-ttu-id="e63fe-198">To access resources in your subscription, you must assign the application to a role.</span><span class="sxs-lookup"><span data-stu-id="e63fe-198">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="e63fe-199">Decide which role represents the right permissions for the application.</span><span class="sxs-lookup"><span data-stu-id="e63fe-199">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="e63fe-200">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e63fe-200">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="e63fe-201">You can set the scope at the level of the subscription, resource group, or resource.</span><span class="sxs-lookup"><span data-stu-id="e63fe-201">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="e63fe-202">Permissions are inherited to lower levels of scope.</span><span class="sxs-lookup"><span data-stu-id="e63fe-202">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="e63fe-203">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span><span class="sxs-lookup"><span data-stu-id="e63fe-203">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="e63fe-204">Navigate to the level of scope you wish to assign the application to.</span><span class="sxs-lookup"><span data-stu-id="e63fe-204">Navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="e63fe-205">For example, to assign a role at the subscription scope, select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-205">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="e63fe-206">You could instead select a resource group or resource.</span><span class="sxs-lookup"><span data-stu-id="e63fe-206">You could instead select a resource group or resource.</span></span>

     ![select subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-subscription.png)

2. <span data-ttu-id="e63fe-208">Select the particular subscription (resource group or resource) to assign the application to.</span><span class="sxs-lookup"><span data-stu-id="e63fe-208">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

     ![select subscription for assignment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. <span data-ttu-id="e63fe-210">Select **Access Control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-210">Select **Access Control (IAM)**.</span></span>

     ![select access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-access-control.png)

4. <span data-ttu-id="e63fe-212">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="e63fe-212">Select **Add**.</span></span>

     ![select add](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-add.png)
6. <span data-ttu-id="e63fe-214">Select the role you wish to assign to the application.</span><span class="sxs-lookup"><span data-stu-id="e63fe-214">Select the role you wish to assign to the application.</span></span> <span data-ttu-id="e63fe-215">The following image shows the **Reader** role.</span><span class="sxs-lookup"><span data-stu-id="e63fe-215">The following image shows the **Reader** role.</span></span>

     ![select role](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/select-role.png)

8. <span data-ttu-id="e63fe-217">Search for your application, and select it.</span><span class="sxs-lookup"><span data-stu-id="e63fe-217">Search for your application, and select it.</span></span>

     ![search for app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-create-service-principal-portal/search-app.png)
9. <span data-ttu-id="e63fe-219">Select **OK** to finish assigning the role.</span><span class="sxs-lookup"><span data-stu-id="e63fe-219">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="e63fe-220">You see your application in the list of users assigned to a role for that scope.</span><span class="sxs-lookup"><span data-stu-id="e63fe-220">You see your application in the list of users assigned to a role for that scope.</span></span>

## <a name="log-in-as-the-application"></a><span data-ttu-id="e63fe-221">Log in as the application</span><span class="sxs-lookup"><span data-stu-id="e63fe-221">Log in as the application</span></span>

<span data-ttu-id="e63fe-222">Your application is now set up in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e63fe-222">Your application is now set up in Azure Active Directory.</span></span> <span data-ttu-id="e63fe-223">You have an ID and key to use for signing in as the application.</span><span class="sxs-lookup"><span data-stu-id="e63fe-223">You have an ID and key to use for signing in as the application.</span></span> <span data-ttu-id="e63fe-224">The application is assigned to a role that gives it certain actions it can perform.</span><span class="sxs-lookup"><span data-stu-id="e63fe-224">The application is assigned to a role that gives it certain actions it can perform.</span></span> 

<span data-ttu-id="e63fe-225">To log in through PowerShell, see [Provide credentials through PowerShell](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell).</span><span class="sxs-lookup"><span data-stu-id="e63fe-225">To log in through PowerShell, see [Provide credentials through PowerShell](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell).</span></span>

<span data-ttu-id="e63fe-226">To log in through Azure CLI, see [Provide credentials through Azure CLI](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e63fe-226">To log in through Azure CLI, see [Provide credentials through Azure CLI](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli).</span></span>

<span data-ttu-id="e63fe-227">To get the access token for REST operations, see [Create the request](/rest/api/#create-the-request).</span><span class="sxs-lookup"><span data-stu-id="e63fe-227">To get the access token for REST operations, see [Create the request](/rest/api/#create-the-request).</span></span>

<span data-ttu-id="e63fe-228">Look at the following sample applications to learn about logging in through application code.</span><span class="sxs-lookup"><span data-stu-id="e63fe-228">Look at the following sample applications to learn about logging in through application code.</span></span>

### <a name="sample-applications"></a><span data-ttu-id="e63fe-229">Sample applications</span><span class="sxs-lookup"><span data-stu-id="e63fe-229">Sample applications</span></span>
<span data-ttu-id="e63fe-230">The following sample applications show how to log in as the AD application.</span><span class="sxs-lookup"><span data-stu-id="e63fe-230">The following sample applications show how to log in as the AD application.</span></span>

<span data-ttu-id="e63fe-231">**.NET**</span><span class="sxs-lookup"><span data-stu-id="e63fe-231">**.NET**</span></span>

* [<span data-ttu-id="e63fe-232">Deploy an SSH Enabled VM with a Template with .NET</span><span class="sxs-lookup"><span data-stu-id="e63fe-232">Deploy an SSH Enabled VM with a Template with .NET</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-dotnet-template-deployment/)
* [<span data-ttu-id="e63fe-233">Manage Azure resources and resource groups with .NET</span><span class="sxs-lookup"><span data-stu-id="e63fe-233">Manage Azure resources and resource groups with .NET</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-dotnet-resources-and-groups/)

<span data-ttu-id="e63fe-234">**Java**</span><span class="sxs-lookup"><span data-stu-id="e63fe-234">**Java**</span></span>

* [<span data-ttu-id="e63fe-235">Getting Started with Resources - Deploy Using Azure Resource Manager Template - in Java</span><span class="sxs-lookup"><span data-stu-id="e63fe-235">Getting Started with Resources - Deploy Using Azure Resource Manager Template - in Java</span></span>](https://azure.microsoft.com/documentation/samples/resources-java-deploy-using-arm-template/)
* [<span data-ttu-id="e63fe-236">Getting Started with Resources - Manage Resource Group - in Java</span><span class="sxs-lookup"><span data-stu-id="e63fe-236">Getting Started with Resources - Manage Resource Group - in Java</span></span>](https://azure.microsoft.com/documentation/samples/resources-java-manage-resource-group//)

<span data-ttu-id="e63fe-237">**Python**</span><span class="sxs-lookup"><span data-stu-id="e63fe-237">**Python**</span></span>

* [<span data-ttu-id="e63fe-238">Deploy an SSH Enabled VM with a Template in Python</span><span class="sxs-lookup"><span data-stu-id="e63fe-238">Deploy an SSH Enabled VM with a Template in Python</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-python-template-deployment/)
* [<span data-ttu-id="e63fe-239">Managing Azure Resource and Resource Groups with Python</span><span class="sxs-lookup"><span data-stu-id="e63fe-239">Managing Azure Resource and Resource Groups with Python</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-python-resources-and-groups/)

<span data-ttu-id="e63fe-240">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="e63fe-240">**Node.js**</span></span>

* [<span data-ttu-id="e63fe-241">Deploy an SSH Enabled VM with a Template in Node.js</span><span class="sxs-lookup"><span data-stu-id="e63fe-241">Deploy an SSH Enabled VM with a Template in Node.js</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-node-template-deployment/)
* [<span data-ttu-id="e63fe-242">Manage Azure resources and resource groups with Node.js</span><span class="sxs-lookup"><span data-stu-id="e63fe-242">Manage Azure resources and resource groups with Node.js</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-node-resources-and-groups/)

<span data-ttu-id="e63fe-243">**Ruby**</span><span class="sxs-lookup"><span data-stu-id="e63fe-243">**Ruby**</span></span>

* [<span data-ttu-id="e63fe-244">Deploy an SSH Enabled VM with a Template in Ruby</span><span class="sxs-lookup"><span data-stu-id="e63fe-244">Deploy an SSH Enabled VM with a Template in Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-template-deployment/)
* [<span data-ttu-id="e63fe-245">Managing Azure Resource and Resource Groups with Ruby</span><span class="sxs-lookup"><span data-stu-id="e63fe-245">Managing Azure Resource and Resource Groups with Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="e63fe-246">Next Steps</span><span class="sxs-lookup"><span data-stu-id="e63fe-246">Next Steps</span></span>
* <span data-ttu-id="e63fe-247">To set up a multi-tenant application, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e63fe-247">To set up a multi-tenant application, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="e63fe-248">To learn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e63fe-248">To learn about specifying security policies, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>  





























