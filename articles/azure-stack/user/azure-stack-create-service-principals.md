---
title: Create a Service Principal for Azure Stack | Microsoft Docs
description: Describes how to create a service principal that can be used with the role-based access control in Azure Resource Manager to manage access to resources.
services: azure-resource-manager
documentationcenter: na
author: sethmanheim
manager: femila
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2018
ms.author: sethm
ms.reviewer: thoroet
ms.openlocfilehash: 77940a52c0817b9eaf49cdf7d1a2d284c5e662e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967147"
---
# <a name="give-applications-access-to-azure-stack-resources-by-creating-service-principals"></a><span data-ttu-id="636ae-103">Give applications access to Azure Stack resources by creating service principals</span><span class="sxs-lookup"><span data-stu-id="636ae-103">Give applications access to Azure Stack resources by creating service principals</span></span>

<span data-ttu-id="636ae-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="636ae-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="636ae-105">You can give an application access to Azure Stack resources by creating a service principal that uses Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="636ae-105">You can give an application access to Azure Stack resources by creating a service principal that uses Azure Resource Manager.</span></span> <span data-ttu-id="636ae-106">A service principal lets you delegate specific permissions using [role-based access control](azure-stack-manage-permissions.md).</span><span class="sxs-lookup"><span data-stu-id="636ae-106">A service principal lets you delegate specific permissions using [role-based access control](azure-stack-manage-permissions.md).</span></span>

<span data-ttu-id="636ae-107">As a best practice, you should use service principals for your applications.</span><span class="sxs-lookup"><span data-stu-id="636ae-107">As a best practice, you should use service principals for your applications.</span></span> <span data-ttu-id="636ae-108">Service principals are preferable to running an app using your own credentials for the following reasons:</span><span class="sxs-lookup"><span data-stu-id="636ae-108">Service principals are preferable to running an app using your own credentials for the following reasons:</span></span>

* <span data-ttu-id="636ae-109">You can assign permissions to the service principal that are different than your own account permissions.</span><span class="sxs-lookup"><span data-stu-id="636ae-109">You can assign permissions to the service principal that are different than your own account permissions.</span></span> <span data-ttu-id="636ae-110">Typically, a service principal's permissions are restricted to exactly what the app needs to do.</span><span class="sxs-lookup"><span data-stu-id="636ae-110">Typically, a service principal's permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="636ae-111">You do not have to change the app's credentials if your role or responsibilities change.</span><span class="sxs-lookup"><span data-stu-id="636ae-111">You do not have to change the app's credentials if your role or responsibilities change.</span></span>
* <span data-ttu-id="636ae-112">You can use a certificate to automate authentication when running an unattended script.</span><span class="sxs-lookup"><span data-stu-id="636ae-112">You can use a certificate to automate authentication when running an unattended script.</span></span>

## <a name="example-scenario"></a><span data-ttu-id="636ae-113">Example scenario</span><span class="sxs-lookup"><span data-stu-id="636ae-113">Example scenario</span></span>

<span data-ttu-id="636ae-114">You have a configuration management app that needs to inventory Azure resources using Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="636ae-114">You have a configuration management app that needs to inventory Azure resources using Azure Resource Manager.</span></span> <span data-ttu-id="636ae-115">You can create a service principal and assign it to the Reader role.</span><span class="sxs-lookup"><span data-stu-id="636ae-115">You can create a service principal and assign it to the Reader role.</span></span> <span data-ttu-id="636ae-116">This role gives the app read-only access to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="636ae-116">This role gives the app read-only access to Azure resources.</span></span>

## <a name="getting-started"></a><span data-ttu-id="636ae-117">Getting started</span><span class="sxs-lookup"><span data-stu-id="636ae-117">Getting started</span></span>

<span data-ttu-id="636ae-118">Use the steps in this article as a guide to:</span><span class="sxs-lookup"><span data-stu-id="636ae-118">Use the steps in this article as a guide to:</span></span>

* <span data-ttu-id="636ae-119">Create a service principal for your app.</span><span class="sxs-lookup"><span data-stu-id="636ae-119">Create a service principal for your app.</span></span>
* <span data-ttu-id="636ae-120">Register your app and create an authentication key.</span><span class="sxs-lookup"><span data-stu-id="636ae-120">Register your app and create an authentication key.</span></span>
* <span data-ttu-id="636ae-121">Assign your app to a role.</span><span class="sxs-lookup"><span data-stu-id="636ae-121">Assign your app to a role.</span></span>

<span data-ttu-id="636ae-122">The way you configured Active Directory for Azure Stack determines how you create a service principal.</span><span class="sxs-lookup"><span data-stu-id="636ae-122">The way you configured Active Directory for Azure Stack determines how you create a service principal.</span></span> <span data-ttu-id="636ae-123">Pick one of the following options:</span><span class="sxs-lookup"><span data-stu-id="636ae-123">Pick one of the following options:</span></span>

* <span data-ttu-id="636ae-124">Create a service principal for [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="636ae-124">Create a service principal for [Azure Active Directory (Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad).</span></span>
* <span data-ttu-id="636ae-125">Create a service principal for [Active Directory Federation Services (AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="636ae-125">Create a service principal for [Active Directory Federation Services (AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span></span>

<span data-ttu-id="636ae-126">The steps for assigning a service principal to a role the same for Azure AD and AD FS.</span><span class="sxs-lookup"><span data-stu-id="636ae-126">The steps for assigning a service principal to a role the same for Azure AD and AD FS.</span></span> <span data-ttu-id="636ae-127">After you create the service principal, you can [delegate permissions](azure-stack-create-service-principals.md#assign-role-to-service-principal) by assigning it to a role.</span><span class="sxs-lookup"><span data-stu-id="636ae-127">After you create the service principal, you can [delegate permissions](azure-stack-create-service-principals.md#assign-role-to-service-principal) by assigning it to a role.</span></span>

## <a name="create-a-service-principal-for-azure-ad"></a><span data-ttu-id="636ae-128">Create a service principal for Azure AD</span><span class="sxs-lookup"><span data-stu-id="636ae-128">Create a service principal for Azure AD</span></span>

<span data-ttu-id="636ae-129">If your Azure Stack uses Azure AD as the identity store, you can create a service principal using the same steps as in Azure, using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="636ae-129">If your Azure Stack uses Azure AD as the identity store, you can create a service principal using the same steps as in Azure, using the Azure portal.</span></span>

>[!NOTE]
<span data-ttu-id="636ae-130">Check to see that you have the [required Azure AD permissions](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) before you start creating a service principal.</span><span class="sxs-lookup"><span data-stu-id="636ae-130">Check to see that you have the [required Azure AD permissions](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) before you start creating a service principal.</span></span>

### <a name="create-service-principal"></a><span data-ttu-id="636ae-131">Create service principal</span><span class="sxs-lookup"><span data-stu-id="636ae-131">Create service principal</span></span>

<span data-ttu-id="636ae-132">To create a service principal for your application:</span><span class="sxs-lookup"><span data-stu-id="636ae-132">To create a service principal for your application:</span></span>

1. <span data-ttu-id="636ae-133">Sign in to your Azure Account through the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="636ae-133">Sign in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="636ae-134">Select **Azure Active Directory** > **App registrations** > **Add**.</span><span class="sxs-lookup"><span data-stu-id="636ae-134">Select **Azure Active Directory** > **App registrations** > **Add**.</span></span>
3. <span data-ttu-id="636ae-135">Provide a name and URL for the application.</span><span class="sxs-lookup"><span data-stu-id="636ae-135">Provide a name and URL for the application.</span></span> <span data-ttu-id="636ae-136">Select either **Web app / API** or **Native** for the type of application you want to create.</span><span class="sxs-lookup"><span data-stu-id="636ae-136">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="636ae-137">After setting the values, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="636ae-137">After setting the values, select **Create**.</span></span>

### <a name="get-credentials"></a><span data-ttu-id="636ae-138">Get credentials</span><span class="sxs-lookup"><span data-stu-id="636ae-138">Get credentials</span></span>

<span data-ttu-id="636ae-139">When logging in programmatically, use the ID for your application and an authentication key.</span><span class="sxs-lookup"><span data-stu-id="636ae-139">When logging in programmatically, use the ID for your application and an authentication key.</span></span> <span data-ttu-id="636ae-140">To get these values:</span><span class="sxs-lookup"><span data-stu-id="636ae-140">To get these values:</span></span>

1. <span data-ttu-id="636ae-141">From **App registrations** in Active Directory, select your application.</span><span class="sxs-lookup"><span data-stu-id="636ae-141">From **App registrations** in Active Directory, select your application.</span></span>

2. <span data-ttu-id="636ae-142">Copy the **Application ID** and store it in your application code.</span><span class="sxs-lookup"><span data-stu-id="636ae-142">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="636ae-143">The applications in the [sample applications](#sample-applications) use **client id** when referring to the **Application ID**.</span><span class="sxs-lookup"><span data-stu-id="636ae-143">The applications in the [sample applications](#sample-applications) use **client id** when referring to the **Application ID**.</span></span>

     ![Application ID for the application](./media/azure-stack-create-service-principal/image12.png)
3. <span data-ttu-id="636ae-145">To generate an authentication key, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="636ae-145">To generate an authentication key, select **Keys**.</span></span>

4. <span data-ttu-id="636ae-146">Provide a description of the key, and a duration for the key.</span><span class="sxs-lookup"><span data-stu-id="636ae-146">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="636ae-147">When done, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="636ae-147">When done, select **Save**.</span></span>

>[!IMPORTANT]
<span data-ttu-id="636ae-148">After you save the key, the key **VALUE** is displayed.</span><span class="sxs-lookup"><span data-stu-id="636ae-148">After you save the key, the key **VALUE** is displayed.</span></span> <span data-ttu-id="636ae-149">Write down this value because you can't retrieve the key later.</span><span class="sxs-lookup"><span data-stu-id="636ae-149">Write down this value because you can't retrieve the key later.</span></span> <span data-ttu-id="636ae-150">Store the key value where your application can retrieve it.</span><span class="sxs-lookup"><span data-stu-id="636ae-150">Store the key value where your application can retrieve it.</span></span>

![Key value warning for saved key.](./media/azure-stack-create-service-principal/image15.png)

<span data-ttu-id="636ae-152">The final step is [assigning your application a role](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span><span class="sxs-lookup"><span data-stu-id="636ae-152">The final step is [assigning your application a role](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span></span>

## <a name="create-service-principal-for-ad-fs"></a><span data-ttu-id="636ae-153">Create service principal for AD FS</span><span class="sxs-lookup"><span data-stu-id="636ae-153">Create service principal for AD FS</span></span>

<span data-ttu-id="636ae-154">If you deployed Azure Stack using AD FS as the identity store, you can use PowerShell for the following tasks:</span><span class="sxs-lookup"><span data-stu-id="636ae-154">If you deployed Azure Stack using AD FS as the identity store, you can use PowerShell for the following tasks:</span></span>

* <span data-ttu-id="636ae-155">Create a service principal.</span><span class="sxs-lookup"><span data-stu-id="636ae-155">Create a service principal.</span></span>
* <span data-ttu-id="636ae-156">Assign service principal to a role.</span><span class="sxs-lookup"><span data-stu-id="636ae-156">Assign service principal to a role.</span></span>
* <span data-ttu-id="636ae-157">Sign in using the service principal's identity.</span><span class="sxs-lookup"><span data-stu-id="636ae-157">Sign in using the service principal's identity.</span></span>

<span data-ttu-id="636ae-158">For details on how to create the service principal, see [Create service principal for AD FS](../azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="636ae-158">For details on how to create the service principal, see [Create service principal for AD FS](../azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span></span>

## <a name="assign-the-service-principal-to-a-role"></a><span data-ttu-id="636ae-159">Assign the service principal to a role</span><span class="sxs-lookup"><span data-stu-id="636ae-159">Assign the service principal to a role</span></span>

<span data-ttu-id="636ae-160">To access resources in your subscription, you must assign the application to a role.</span><span class="sxs-lookup"><span data-stu-id="636ae-160">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="636ae-161">Decide which role represents the right permissions for the application.</span><span class="sxs-lookup"><span data-stu-id="636ae-161">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="636ae-162">To learn about the available roles, see [RBAC: Built in Roles](../../role-based-access-control/built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="636ae-162">To learn about the available roles, see [RBAC: Built in Roles](../../role-based-access-control/built-in-roles.md).</span></span>

>[!NOTE]
<span data-ttu-id="636ae-163">You can set a role's scope at the level of a subscription, a resource group, or a resource.</span><span class="sxs-lookup"><span data-stu-id="636ae-163">You can set a role's scope at the level of a subscription, a resource group, or a resource.</span></span> <span data-ttu-id="636ae-164">Permissions are inherited to lower levels of scope.</span><span class="sxs-lookup"><span data-stu-id="636ae-164">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="636ae-165">For example, an app with the Reader role for a resource group means that the app can read any of the resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="636ae-165">For example, an app with the Reader role for a resource group means that the app can read any of the resources in the resource group.</span></span>

<span data-ttu-id="636ae-166">Use the following steps as a guide for assigning a role to a service principal.</span><span class="sxs-lookup"><span data-stu-id="636ae-166">Use the following steps as a guide for assigning a role to a service principal.</span></span>

1. <span data-ttu-id="636ae-167">In the Azure Stack portal, navigate to the level of scope you want to assign the application to.</span><span class="sxs-lookup"><span data-stu-id="636ae-167">In the Azure Stack portal, navigate to the level of scope you want to assign the application to.</span></span> <span data-ttu-id="636ae-168">For example, to assign a role at the subscription scope, select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="636ae-168">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span>

2. <span data-ttu-id="636ae-169">Select the subscription to assign the application to.</span><span class="sxs-lookup"><span data-stu-id="636ae-169">Select the subscription to assign the application to.</span></span> <span data-ttu-id="636ae-170">In this example, the subscription is Visual Studio Enterprise.</span><span class="sxs-lookup"><span data-stu-id="636ae-170">In this example, the subscription is Visual Studio Enterprise.</span></span>

     ![Select Visual Studio Enterprise subscription for assignment](./media/azure-stack-create-service-principal/image16.png)

3. <span data-ttu-id="636ae-172">Select **Access Control (IAM)** for the subscription.</span><span class="sxs-lookup"><span data-stu-id="636ae-172">Select **Access Control (IAM)** for the subscription.</span></span>

     ![Select Access control](./media/azure-stack-create-service-principal/image17.png)

4. <span data-ttu-id="636ae-174">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="636ae-174">Select **Add**.</span></span>

5. <span data-ttu-id="636ae-175">Select the role you wish to assign to the application.</span><span class="sxs-lookup"><span data-stu-id="636ae-175">Select the role you wish to assign to the application.</span></span>

6. <span data-ttu-id="636ae-176">Search for your application, and select it.</span><span class="sxs-lookup"><span data-stu-id="636ae-176">Search for your application, and select it.</span></span>

7. <span data-ttu-id="636ae-177">Select **OK** to finish assigning the role.</span><span class="sxs-lookup"><span data-stu-id="636ae-177">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="636ae-178">You can see your application in the list of users assigned to a role for that scope.</span><span class="sxs-lookup"><span data-stu-id="636ae-178">You can see your application in the list of users assigned to a role for that scope.</span></span>

<span data-ttu-id="636ae-179">Now that you've created a service principal and assigned a role, your application can access Azure Stack resources.</span><span class="sxs-lookup"><span data-stu-id="636ae-179">Now that you've created a service principal and assigned a role, your application can access Azure Stack resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="636ae-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="636ae-180">Next steps</span></span>

[<span data-ttu-id="636ae-181">Manage user permissions</span><span class="sxs-lookup"><span data-stu-id="636ae-181">Manage user permissions</span></span>](azure-stack-manage-permissions.md)
