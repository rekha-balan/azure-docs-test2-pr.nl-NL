---
title: Create a Service Principal for Azure Stack | Microsoft Docs
description: Describes how to create a new service principal that can be used with the role-based access control in Azure Resource Manager to manage access to resources.
services: azure-resource-manager
documentationcenter: na
author: Shriramnat
manager: bradleyb
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: shnatara
ms.openlocfilehash: 1a06fb086438ec18c7608fcbf968ab9ec818d580
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551644"
---
# <a name="provide-applications-access-to-azure-stack"></a><span data-ttu-id="75a9a-103">Provide applications access to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="75a9a-103">Provide applications access to Azure Stack</span></span>
<span data-ttu-id="75a9a-104">When an application needs access to deploy or configure resources through Azure Resource Manager in Azure Stack, you will create a service principal, which is an identity for your application.</span><span class="sxs-lookup"><span data-stu-id="75a9a-104">When an application needs access to deploy or configure resources through Azure Resource Manager in Azure Stack, you will create a service principal, which is an identity for your application.</span></span>  <span data-ttu-id="75a9a-105">You can then delegate only the necessary permissions to that service principal.</span><span class="sxs-lookup"><span data-stu-id="75a9a-105">You can then delegate only the necessary permissions to that service principal.</span></span>  

<span data-ttu-id="75a9a-106">As an example, you may have a configuration management tool that uses Azure Resource Manager to inventory resources.</span><span class="sxs-lookup"><span data-stu-id="75a9a-106">As an example, you may have a configuration management tool that uses Azure Resource Manager to inventory resources.</span></span>  <span data-ttu-id="75a9a-107">In this scenario, you can create a service principal, grant the reader role to that service principal, and limit the configuration management tool to read-only access.</span><span class="sxs-lookup"><span data-stu-id="75a9a-107">In this scenario, you can create a service principal, grant the reader role to that service principal, and limit the configuration management tool to read-only access.</span></span> 

<span data-ttu-id="75a9a-108">Service principals are preferable to running the app under your own credentials because:</span><span class="sxs-lookup"><span data-stu-id="75a9a-108">Service principals are preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="75a9a-109">You can assign permissions to the service principal that are different than your own account permissions.</span><span class="sxs-lookup"><span data-stu-id="75a9a-109">You can assign permissions to the service principal that are different than your own account permissions.</span></span> <span data-ttu-id="75a9a-110">Typically, these permissions are restricted to exactly what the app needs to do.</span><span class="sxs-lookup"><span data-stu-id="75a9a-110">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="75a9a-111">You do not have to change the app's credentials if your responsibilities change.</span><span class="sxs-lookup"><span data-stu-id="75a9a-111">You do not have to change the app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="75a9a-112">You can use a certificate to automate authentication when executing an unattended script.</span><span class="sxs-lookup"><span data-stu-id="75a9a-112">You can use a certificate to automate authentication when executing an unattended script.</span></span>  

## <a name="getting-started"></a><span data-ttu-id="75a9a-113">Getting started</span><span class="sxs-lookup"><span data-stu-id="75a9a-113">Getting started</span></span>

<span data-ttu-id="75a9a-114">Depending on how you have deployed Azure Stack, you will start by creating a service principal.</span><span class="sxs-lookup"><span data-stu-id="75a9a-114">Depending on how you have deployed Azure Stack, you will start by creating a service principal.</span></span>  <span data-ttu-id="75a9a-115">This document guides you through creating a service principal for both [Azure Active Directory(Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) and [Active Directory Federation Services(AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="75a9a-115">This document guides you through creating a service principal for both [Azure Active Directory(Azure AD)](azure-stack-create-service-principals.md#create-service-principal-for-azure-ad) and [Active Directory Federation Services(AD FS)](azure-stack-create-service-principals.md#create-service-principal-for-ad-fs).</span></span>  <span data-ttu-id="75a9a-116">Once you've created the service principal, you'll use a set of steps that are common to both AD FS and Azure AD to [delegate permissions](azure-stack-create-service-principals.md#assign-role-to-service-principal) to the role.</span><span class="sxs-lookup"><span data-stu-id="75a9a-116">Once you've created the service principal, you'll use a set of steps that are common to both AD FS and Azure AD to [delegate permissions](azure-stack-create-service-principals.md#assign-role-to-service-principal) to the role.</span></span>     

## <a name="create-service-principal-for-azure-ad"></a><span data-ttu-id="75a9a-117">Create service principal for Azure AD</span><span class="sxs-lookup"><span data-stu-id="75a9a-117">Create service principal for Azure AD</span></span>

<span data-ttu-id="75a9a-118">If you've deployed Azure Stack using Azure AD as the identity store, you can create service principals just like you do for Azure.</span><span class="sxs-lookup"><span data-stu-id="75a9a-118">If you've deployed Azure Stack using Azure AD as the identity store, you can create service principals just like you do for Azure.</span></span>  <span data-ttu-id="75a9a-119">This section shows you how to perform the steps through the portal.</span><span class="sxs-lookup"><span data-stu-id="75a9a-119">This section shows you how to perform the steps through the portal.</span></span>  <span data-ttu-id="75a9a-120">Check that you have the [required Azure AD permissions](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) before beginning.</span><span class="sxs-lookup"><span data-stu-id="75a9a-120">Check that you have the [required Azure AD permissions](../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions) before beginning.</span></span>

### <a name="create-service-principal"></a><span data-ttu-id="75a9a-121">Create service principal</span><span class="sxs-lookup"><span data-stu-id="75a9a-121">Create service principal</span></span>
<span data-ttu-id="75a9a-122">In this section, you'll create an application (service principal) in Azure AD that will represent your application.</span><span class="sxs-lookup"><span data-stu-id="75a9a-122">In this section, you'll create an application (service principal) in Azure AD that will represent your application.</span></span>

1. <span data-ttu-id="75a9a-123">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="75a9a-123">Log in to your Azure Account through the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="75a9a-124">Select **Azure Active Directory** > **App registrations** > **Add**</span><span class="sxs-lookup"><span data-stu-id="75a9a-124">Select **Azure Active Directory** > **App registrations** > **Add**</span></span>   
3. <span data-ttu-id="75a9a-125">Provide a name and URL for the application.</span><span class="sxs-lookup"><span data-stu-id="75a9a-125">Provide a name and URL for the application.</span></span> <span data-ttu-id="75a9a-126">Select either **Web app / API** or **Native** for the type of application you want to create.</span><span class="sxs-lookup"><span data-stu-id="75a9a-126">Select either **Web app / API** or **Native** for the type of application you want to create.</span></span> <span data-ttu-id="75a9a-127">After setting the values, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="75a9a-127">After setting the values, select **Create**.</span></span>

<span data-ttu-id="75a9a-128">You have created a service principal for your application.</span><span class="sxs-lookup"><span data-stu-id="75a9a-128">You have created a service principal for your application.</span></span>

### <a name="get-credentials"></a><span data-ttu-id="75a9a-129">Get credentials</span><span class="sxs-lookup"><span data-stu-id="75a9a-129">Get credentials</span></span>
<span data-ttu-id="75a9a-130">When programmatically logging in, you use the ID for your application and an authentication key.</span><span class="sxs-lookup"><span data-stu-id="75a9a-130">When programmatically logging in, you use the ID for your application and an authentication key.</span></span> <span data-ttu-id="75a9a-131">To get those values, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="75a9a-131">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="75a9a-132">From **App registrations** in Active Directory, select your application.</span><span class="sxs-lookup"><span data-stu-id="75a9a-132">From **App registrations** in Active Directory, select your application.</span></span>

2. <span data-ttu-id="75a9a-133">Copy the **Application ID** and store it in your application code.</span><span class="sxs-lookup"><span data-stu-id="75a9a-133">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="75a9a-134">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span><span class="sxs-lookup"><span data-stu-id="75a9a-134">The applications in the [sample applications](#sample-applications) section refer to this value as the client id.</span></span>

     ![client id](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-service-principal/image12.png)
3. <span data-ttu-id="75a9a-136">To generate an authentication key, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="75a9a-136">To generate an authentication key, select **Keys**.</span></span>

4. <span data-ttu-id="75a9a-137">Provide a description of the key, and a duration for the key.</span><span class="sxs-lookup"><span data-stu-id="75a9a-137">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="75a9a-138">When done, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="75a9a-138">When done, select **Save**.</span></span>

<span data-ttu-id="75a9a-139">After saving the key, the value of the key is displayed.</span><span class="sxs-lookup"><span data-stu-id="75a9a-139">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="75a9a-140">Copy this value because you are not able to retrieve the key later.</span><span class="sxs-lookup"><span data-stu-id="75a9a-140">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="75a9a-141">You provide the key value with the application ID to sign as the application.</span><span class="sxs-lookup"><span data-stu-id="75a9a-141">You provide the key value with the application ID to sign as the application.</span></span> <span data-ttu-id="75a9a-142">Store the key value where your application can retrieve it.</span><span class="sxs-lookup"><span data-stu-id="75a9a-142">Store the key value where your application can retrieve it.</span></span>

![saved key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-service-principal/image15.png)


<span data-ttu-id="75a9a-144">Once complete, proceed to [assigning your application a role](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span><span class="sxs-lookup"><span data-stu-id="75a9a-144">Once complete, proceed to [assigning your application a role](azure-stack-create-service-principals.md#assign-role-to-service-principal).</span></span>

## <a name="create-service-principal-for-ad-fs"></a><span data-ttu-id="75a9a-145">Create service principal for AD FS</span><span class="sxs-lookup"><span data-stu-id="75a9a-145">Create service principal for AD FS</span></span>
<span data-ttu-id="75a9a-146">If you have deployed Azure Stack with AD FS, you can use PowerShell to create a service principal, assign a role for access, and sign in from PowerShell using that identity.</span><span class="sxs-lookup"><span data-stu-id="75a9a-146">If you have deployed Azure Stack with AD FS, you can use PowerShell to create a service principal, assign a role for access, and sign in from PowerShell using that identity.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="75a9a-147">Before you begin</span><span class="sxs-lookup"><span data-stu-id="75a9a-147">Before you begin</span></span>

[<span data-ttu-id="75a9a-148">Download the tools required to work with Azure Stack to your local computer.</span><span class="sxs-lookup"><span data-stu-id="75a9a-148">Download the tools required to work with Azure Stack to your local computer.</span></span>](azure-stack-powershell-download.md)

### <a name="import-the-identity-powershell-module"></a><span data-ttu-id="75a9a-149">Import the Identity PowerShell module</span><span class="sxs-lookup"><span data-stu-id="75a9a-149">Import the Identity PowerShell module</span></span>
<span data-ttu-id="75a9a-150">After you download the tools, navigate to the downloaded folder and import the Identity PowerShell module by using the following command:</span><span class="sxs-lookup"><span data-stu-id="75a9a-150">After you download the tools, navigate to the downloaded folder and import the Identity PowerShell module by using the following command:</span></span>

```PowerShell
Import-Module .\Identity\AzureStack.Identity.psm1
```

<span data-ttu-id="75a9a-151">When you import the module, you may receive an error that says “AzureStack.Connect.psm1 is not digitally signed.</span><span class="sxs-lookup"><span data-stu-id="75a9a-151">When you import the module, you may receive an error that says “AzureStack.Connect.psm1 is not digitally signed.</span></span> <span data-ttu-id="75a9a-152">The script will not execute on the system”.</span><span class="sxs-lookup"><span data-stu-id="75a9a-152">The script will not execute on the system”.</span></span> <span data-ttu-id="75a9a-153">To resolve this issue, you can set execution policy to allow running the script with the following command in an elevated PowerShell session:</span><span class="sxs-lookup"><span data-stu-id="75a9a-153">To resolve this issue, you can set execution policy to allow running the script with the following command in an elevated PowerShell session:</span></span>

```PowerShell
Set-ExecutionPolicy Unrestricted
```

### <a name="create-the-service-principal"></a><span data-ttu-id="75a9a-154">Create the service principal</span><span class="sxs-lookup"><span data-stu-id="75a9a-154">Create the service principal</span></span>
<span data-ttu-id="75a9a-155">You can create a Service Principal by executing the following command:</span><span class="sxs-lookup"><span data-stu-id="75a9a-155">You can create a Service Principal by executing the following command:</span></span>
```powershell
$servicePrincipal = New-ADGraphServicePrincipal`
 -DisplayName "<YourServicePrincipalName>"`
 -AdminCredential $(Get-Credential)`
 -Verbose
```
### <a name="assign-a-role"></a><span data-ttu-id="75a9a-156">Assign a role</span><span class="sxs-lookup"><span data-stu-id="75a9a-156">Assign a role</span></span>
<span data-ttu-id="75a9a-157">Once the Service Principal is created, you must [assign it to a role](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span><span class="sxs-lookup"><span data-stu-id="75a9a-157">Once the Service Principal is created, you must [assign it to a role](azure-stack-create-service-principals.md#assign-role-to-service-principal)</span></span>

### <a name="sign-in-through-powershell"></a><span data-ttu-id="75a9a-158">Sign in through PowerShell</span><span class="sxs-lookup"><span data-stu-id="75a9a-158">Sign in through PowerShell</span></span>
<span data-ttu-id="75a9a-159">Once you've assigned a role, you can sign in using the service principal with the following command:</span><span class="sxs-lookup"><span data-stu-id="75a9a-159">Once you've assigned a role, you can sign in using the service principal with the following command:</span></span>

```powershell
Add-AzureRmAccount -EnvironmentName "<AzureStackEnvironmentName>"`
 -ServicePrincipal`
 -CertificateThumbprint $servicePrincipal.Thumbprint`
 -ApplicationId $servicePrincipal.ApplicationId` 
 -TenantId $directoryTenantId
```

## <a name="assign-role-to-service-principal"></a><span data-ttu-id="75a9a-160">Assign role to service principal</span><span class="sxs-lookup"><span data-stu-id="75a9a-160">Assign role to service principal</span></span>
<span data-ttu-id="75a9a-161">To access resources in your subscription, you must assign the application to a role.</span><span class="sxs-lookup"><span data-stu-id="75a9a-161">To access resources in your subscription, you must assign the application to a role.</span></span> <span data-ttu-id="75a9a-162">Decide which role represents the right permissions for the application.</span><span class="sxs-lookup"><span data-stu-id="75a9a-162">Decide which role represents the right permissions for the application.</span></span> <span data-ttu-id="75a9a-163">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="75a9a-163">To learn about the available roles, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="75a9a-164">You can set the scope at the level of the subscription, resource group, or resource.</span><span class="sxs-lookup"><span data-stu-id="75a9a-164">You can set the scope at the level of the subscription, resource group, or resource.</span></span> <span data-ttu-id="75a9a-165">Permissions are inherited to lower levels of scope.</span><span class="sxs-lookup"><span data-stu-id="75a9a-165">Permissions are inherited to lower levels of scope.</span></span> <span data-ttu-id="75a9a-166">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span><span class="sxs-lookup"><span data-stu-id="75a9a-166">For example, adding an application to the Reader role for a resource group means it can read the resource group and any resources it contains.</span></span>

1. <span data-ttu-id="75a9a-167">Navigate to the level of scope you wish to assign the application to.</span><span class="sxs-lookup"><span data-stu-id="75a9a-167">Navigate to the level of scope you wish to assign the application to.</span></span> <span data-ttu-id="75a9a-168">For example, to assign a role at the subscription scope, select **Subscriptions**.</span><span class="sxs-lookup"><span data-stu-id="75a9a-168">For example, to assign a role at the subscription scope, select **Subscriptions**.</span></span> <span data-ttu-id="75a9a-169">You could instead select a resource group or resource.</span><span class="sxs-lookup"><span data-stu-id="75a9a-169">You could instead select a resource group or resource.</span></span>

2. <span data-ttu-id="75a9a-170">Select the particular subscription (resource group or resource) to assign the application to.</span><span class="sxs-lookup"><span data-stu-id="75a9a-170">Select the particular subscription (resource group or resource) to assign the application to.</span></span>

     ![select subscription for assignment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-service-principal/image16.png)

3. <span data-ttu-id="75a9a-172">Select **Access Control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="75a9a-172">Select **Access Control (IAM)**.</span></span>

     ![select access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-create-service-principal/image17.png)

4. <span data-ttu-id="75a9a-174">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="75a9a-174">Select **Add**.</span></span>

5. <span data-ttu-id="75a9a-175">Select the role you wish to assign to the application.</span><span class="sxs-lookup"><span data-stu-id="75a9a-175">Select the role you wish to assign to the application.</span></span>

6. <span data-ttu-id="75a9a-176">Search for your application, and select it.</span><span class="sxs-lookup"><span data-stu-id="75a9a-176">Search for your application, and select it.</span></span>

7. <span data-ttu-id="75a9a-177">Select **OK** to finish assigning the role.</span><span class="sxs-lookup"><span data-stu-id="75a9a-177">Select **OK** to finish assigning the role.</span></span> <span data-ttu-id="75a9a-178">You see your application in the list of users assigned to a role for that scope.</span><span class="sxs-lookup"><span data-stu-id="75a9a-178">You see your application in the list of users assigned to a role for that scope.</span></span>

<span data-ttu-id="75a9a-179">Now that you've created a service principal and assigned a role, you can begin using this within your application to access Azure Stack resources.</span><span class="sxs-lookup"><span data-stu-id="75a9a-179">Now that you've created a service principal and assigned a role, you can begin using this within your application to access Azure Stack resources.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="75a9a-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="75a9a-180">Next steps</span></span>

<span data-ttu-id="75a9a-181">[Add users for ADFS](azure-stack-add-users-adfs.md)
[Manage user permissions](azure-stack-manage-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="75a9a-181">[Add users for ADFS](azure-stack-add-users-adfs.md)
[Manage user permissions](azure-stack-manage-permissions.md)</span></span>



