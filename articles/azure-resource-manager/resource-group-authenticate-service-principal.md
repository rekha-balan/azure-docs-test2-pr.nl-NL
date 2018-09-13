---
title: Create identity for Azure app with PowerShell | Microsoft Docs
description: Describes how to use Azure PowerShell to create an Azure Active Directory application and service principal, and grant it access to resources through role-based access control. It shows how to authenticate application with a password or certificate.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: d2caf121-9fbe-4f00-bf9d-8f3d1f00a6ff
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/03/2017
ms.author: tomfitz
ms.openlocfilehash: 775734ea55d1136e64afc713356b0f0bfc81ea9f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548967"
---
# <a name="use-azure-powershell-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="e2d15-104">Use Azure PowerShell to create a service principal to access resources</span><span class="sxs-lookup"><span data-stu-id="e2d15-104">Use Azure PowerShell to create a service principal to access resources</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-authenticate-service-principal.md)
> * [Azure CLI](resource-group-authenticate-service-principal-cli.md)
> * [Portal](resource-group-create-service-principal-portal.md)
> 
> 

<span data-ttu-id="e2d15-108">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span><span class="sxs-lookup"><span data-stu-id="e2d15-108">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="e2d15-109">This identity is known as a service principal.</span><span class="sxs-lookup"><span data-stu-id="e2d15-109">This identity is known as a service principal.</span></span> <span data-ttu-id="e2d15-110">This approach enables you to:</span><span class="sxs-lookup"><span data-stu-id="e2d15-110">This approach enables you to:</span></span>

* <span data-ttu-id="e2d15-111">Assign permissions to the app identity that are different than your own permissions.</span><span class="sxs-lookup"><span data-stu-id="e2d15-111">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="e2d15-112">Typically, these permissions are restricted to exactly what the app needs to do.</span><span class="sxs-lookup"><span data-stu-id="e2d15-112">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="e2d15-113">Use a certificate for authentication when executing an unattended script.</span><span class="sxs-lookup"><span data-stu-id="e2d15-113">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="e2d15-114">This topic shows you how to use [Azure PowerShell](/powershell/azureps-cmdlets-docs) to set up everything you need for an application to run under its own credentials and identity.</span><span class="sxs-lookup"><span data-stu-id="e2d15-114">This topic shows you how to use [Azure PowerShell](/powershell/azureps-cmdlets-docs) to set up everything you need for an application to run under its own credentials and identity.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="e2d15-115">Required permissions</span><span class="sxs-lookup"><span data-stu-id="e2d15-115">Required permissions</span></span>
<span data-ttu-id="e2d15-116">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e2d15-116">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="e2d15-117">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span><span class="sxs-lookup"><span data-stu-id="e2d15-117">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="e2d15-118">The easiest way to check whether your account has adequate permissions is through the portal.</span><span class="sxs-lookup"><span data-stu-id="e2d15-118">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="e2d15-119">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="e2d15-119">See [Check required permission](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="e2d15-120">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span><span class="sxs-lookup"><span data-stu-id="e2d15-120">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="e2d15-121">Create service principal with password</span><span class="sxs-lookup"><span data-stu-id="e2d15-121">Create service principal with password</span></span>
<span data-ttu-id="e2d15-122">The following script creates an identity for your application, and assigns it to the Contributor role for the specified scope:</span><span class="sxs-lookup"><span data-stu-id="e2d15-122">The following script creates an identity for your application, and assigns it to the Contributor role for the specified scope:</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $Password
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.SubscriptionId
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 # Create Azure Active Directory application with password
 $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $ApplicationDisplayName) -IdentifierUris ("http://" + $ApplicationDisplayName) -Password $Password

 # Create Service Principal for the AD app
 $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId 
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="e2d15-123">A few items to note about the script:</span><span class="sxs-lookup"><span data-stu-id="e2d15-123">A few items to note about the script:</span></span>

* <span data-ttu-id="e2d15-124">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span><span class="sxs-lookup"><span data-stu-id="e2d15-124">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="e2d15-125">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span><span class="sxs-lookup"><span data-stu-id="e2d15-125">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
* <span data-ttu-id="e2d15-126">For single-tenant applications, the home page and identifier URIs are not validated.</span><span class="sxs-lookup"><span data-stu-id="e2d15-126">For single-tenant applications, the home page and identifier URIs are not validated.</span></span>
*  <span data-ttu-id="e2d15-127">In this example, you add the service principal to the Contributor role.</span><span class="sxs-lookup"><span data-stu-id="e2d15-127">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="e2d15-128">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e2d15-128">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="e2d15-129">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2d15-129">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="e2d15-130">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span><span class="sxs-lookup"><span data-stu-id="e2d15-130">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="e2d15-131">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span><span class="sxs-lookup"><span data-stu-id="e2d15-131">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>


### <a name="provide-credentials-through-powershell"></a><span data-ttu-id="e2d15-132">Provide credentials through PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2d15-132">Provide credentials through PowerShell</span></span>
<span data-ttu-id="e2d15-133">Now, you need to log in as the application to perform operations.</span><span class="sxs-lookup"><span data-stu-id="e2d15-133">Now, you need to log in as the application to perform operations.</span></span> <span data-ttu-id="e2d15-134">For the user name, use the `ApplicationId` that you created for the application.</span><span class="sxs-lookup"><span data-stu-id="e2d15-134">For the user name, use the `ApplicationId` that you created for the application.</span></span> <span data-ttu-id="e2d15-135">For the password, use the one you specified when creating the account.</span><span class="sxs-lookup"><span data-stu-id="e2d15-135">For the password, use the one you specified when creating the account.</span></span> 

```powershell   
$creds = Get-Credential
Login-AzureRmAccount -Credential $creds -ServicePrincipal -TenantId {tenant-id}
```

<span data-ttu-id="e2d15-136">The tenant ID is not sensitive, so you can embed it directly in your script.</span><span class="sxs-lookup"><span data-stu-id="e2d15-136">The tenant ID is not sensitive, so you can embed it directly in your script.</span></span> <span data-ttu-id="e2d15-137">If you need to retrieve the tenant ID, use:</span><span class="sxs-lookup"><span data-stu-id="e2d15-137">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

## <a name="create-service-principal-with-self-signed-certificate"></a><span data-ttu-id="e2d15-138">Create service principal with self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="e2d15-138">Create service principal with self-signed certificate</span></span>
<span data-ttu-id="e2d15-139">To generate a self-signed certificate and service principal with Azure PowerShell 2.0 on Windows 10 or Windows Server 2016 Technical Preview, use the following script:</span><span class="sxs-lookup"><span data-stu-id="e2d15-139">To generate a self-signed certificate and service principal with Azure PowerShell 2.0 on Windows 10 or Windows Server 2016 Technical Preview, use the following script:</span></span>

```powershell
Param (

 # Use to set scope to resource group. If no value is provided, scope is set to subscription.
 [Parameter(Mandatory=$false)]
 [String] $ResourceGroup,

 # Use to set subscription. If no value is provided, default subscription is used. 
 [Parameter(Mandatory=$false)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources

 if ($SubscriptionId -eq "") 
 {
    $SubscriptionId = (Get-AzureRmContext).Subscription.SubscriptionId
 }
 else
 {
    Set-AzureRmContext -SubscriptionId $SubscriptionId
 }

 if ($ResourceGroup -eq "")
 {
    $Scope = "/subscriptions/" + $SubscriptionId
 }
 else
 {
    $Scope = (Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop).ResourceId
 }

 $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=exampleappScriptCert" -KeySpec KeyExchange
 $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())

 # Use Key credentials
 $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $ApplicationDisplayName) -IdentifierUris ("http://" + $ApplicationDisplayName) -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore

 $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId 
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
```

<span data-ttu-id="e2d15-140">A few items to note about the script:</span><span class="sxs-lookup"><span data-stu-id="e2d15-140">A few items to note about the script:</span></span>

* <span data-ttu-id="e2d15-141">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span><span class="sxs-lookup"><span data-stu-id="e2d15-141">To grant the identity access to the default subscription, you do not need to provide either ResourceGroup or SubscriptionId parameters.</span></span>
* <span data-ttu-id="e2d15-142">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span><span class="sxs-lookup"><span data-stu-id="e2d15-142">Specify the ResourceGroup parameter only when you want to limit the scope of the role assignment to a resource group.</span></span>
* <span data-ttu-id="e2d15-143">For single-tenant applications, the home page and identifier URIs are not validated.</span><span class="sxs-lookup"><span data-stu-id="e2d15-143">For single-tenant applications, the home page and identifier URIs are not validated.</span></span>
*  <span data-ttu-id="e2d15-144">In this example, you add the service principal to the Contributor role.</span><span class="sxs-lookup"><span data-stu-id="e2d15-144">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="e2d15-145">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e2d15-145">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="e2d15-146">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2d15-146">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="e2d15-147">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span><span class="sxs-lookup"><span data-stu-id="e2d15-147">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="e2d15-148">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span><span class="sxs-lookup"><span data-stu-id="e2d15-148">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

<span data-ttu-id="e2d15-149">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need to download the [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="e2d15-149">If you **do not have Windows 10 or Windows Server 2016 Technical Preview**, you need to download the [Self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from Microsoft Script Center.</span></span> <span data-ttu-id="e2d15-150">Extract its contents and import the cmdlet you need.</span><span class="sxs-lookup"><span data-stu-id="e2d15-150">Extract its contents and import the cmdlet you need.</span></span>

```powershell  
# Only run if you could not use New-SelfSignedCertificate
Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
```
  
<span data-ttu-id="e2d15-151">In the script, substitute the following two lines to generate the certificate.</span><span class="sxs-lookup"><span data-stu-id="e2d15-151">In the script, substitute the following two lines to generate the certificate.</span></span>
  
```powershell
New-SelfSignedCertificateEx  -StoreLocation CurrentUser -StoreName My -Subject "CN=exampleapp" -KeySpec "Exchange" -FriendlyName "exampleapp"
$cert = Get-ChildItem -path Cert:\CurrentUser\my | where {$PSitem.Subject -eq 'CN=exampleapp' }
```

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="e2d15-152">Provide certificate through automated PowerShell script</span><span class="sxs-lookup"><span data-stu-id="e2d15-152">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="e2d15-153">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span><span class="sxs-lookup"><span data-stu-id="e2d15-153">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="e2d15-154">A tenant is an instance of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2d15-154">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="e2d15-155">If you only have one subscription, you can use:</span><span class="sxs-lookup"><span data-stu-id="e2d15-155">If you only have one subscription, you can use:</span></span>

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertSubject,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $Thumbprint = (Get-ChildItem cert:\CurrentUser\My\ | Where-Object {$_.Subject -match $CertSubject }).Thumbprint
 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

<span data-ttu-id="e2d15-156">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span><span class="sxs-lookup"><span data-stu-id="e2d15-156">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="e2d15-157">If you need to retrieve the tenant ID, use:</span><span class="sxs-lookup"><span data-stu-id="e2d15-157">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="e2d15-158">If you need to retrieve the application ID, use:</span><span class="sxs-lookup"><span data-stu-id="e2d15-158">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="create-service-principal-with-certificate-from-certificate-authority"></a><span data-ttu-id="e2d15-159">Create service principal with certificate from Certificate Authority</span><span class="sxs-lookup"><span data-stu-id="e2d15-159">Create service principal with certificate from Certificate Authority</span></span>
<span data-ttu-id="e2d15-160">To use a certificate issued from a Certificate Authority to create service principal, use the following script:</span><span class="sxs-lookup"><span data-stu-id="e2d15-160">To use a certificate issued from a Certificate Authority to create service principal, use the following script:</span></span>

```powershell
Param (
 [Parameter(Mandatory=$true)]
 [String] $ApplicationDisplayName,

 [Parameter(Mandatory=$true)]
 [String] $SubscriptionId,

 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword
 )

 Login-AzureRmAccount
 Import-Module AzureRM.Resources
 Set-AzureRmContext -SubscriptionId $SubscriptionId

 $KeyId = (New-Guid).Guid
 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force

 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $KeyValue = [System.Convert]::ToBase64String($PFXCert.GetRawCertData())

 $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
 $KeyCredential.StartDate = $PFXCert.NotBefore
 $KeyCredential.EndDate= $PFXCert.NotAfter
 $KeyCredential.KeyId = $KeyId
 $KeyCredential.CertValue = $KeyValue

 # Use Key credentials
 $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $ApplicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $keyCredential

 $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId 
 Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 

 $NewRole = $null
 $Retries = 0;
 While ($NewRole -eq $null -and $Retries -le 6)
 {
    # Sleep here for a few seconds to allow the service principal application to become active (should only take a couple of seconds normally)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
 }
 
 $NewRole
```

<span data-ttu-id="e2d15-161">A few items to note about the script:</span><span class="sxs-lookup"><span data-stu-id="e2d15-161">A few items to note about the script:</span></span>

* <span data-ttu-id="e2d15-162">Access is scoped to the subscription.</span><span class="sxs-lookup"><span data-stu-id="e2d15-162">Access is scoped to the subscription.</span></span>
* <span data-ttu-id="e2d15-163">For single-tenant applications, the home page and identifier URIs are not validated.</span><span class="sxs-lookup"><span data-stu-id="e2d15-163">For single-tenant applications, the home page and identifier URIs are not validated.</span></span>
*  <span data-ttu-id="e2d15-164">In this example, you add the service principal to the Contributor role.</span><span class="sxs-lookup"><span data-stu-id="e2d15-164">In this example, you add the service principal to the Contributor role.</span></span> <span data-ttu-id="e2d15-165">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="e2d15-165">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span>
* <span data-ttu-id="e2d15-166">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2d15-166">The script sleeps for 15 seconds to allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="e2d15-167">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span><span class="sxs-lookup"><span data-stu-id="e2d15-167">If your script does not wait long enough, you see an error stating: "PrincipalNotFound: Principal {id} does not exist in the directory."</span></span>
* <span data-ttu-id="e2d15-168">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span><span class="sxs-lookup"><span data-stu-id="e2d15-168">If you need to grant the service principal access to more subscriptions or resource groups, run the `New-AzureRMRoleAssignment` cmdlet again with different scopes.</span></span>

### <a name="provide-certificate-through-automated-powershell-script"></a><span data-ttu-id="e2d15-169">Provide certificate through automated PowerShell script</span><span class="sxs-lookup"><span data-stu-id="e2d15-169">Provide certificate through automated PowerShell script</span></span>
<span data-ttu-id="e2d15-170">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span><span class="sxs-lookup"><span data-stu-id="e2d15-170">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="e2d15-171">A tenant is an instance of Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e2d15-171">A tenant is an instance of Azure Active Directory.</span></span>

```powershell
Param (
 
 [Parameter(Mandatory=$true)]
 [String] $CertPath,

 [Parameter(Mandatory=$true)]
 [String] $CertPlainPassword,
 
 [Parameter(Mandatory=$true)]
 [String] $ApplicationId,

 [Parameter(Mandatory=$true)]
 [String] $TenantId
 )

 $CertPassword = ConvertTo-SecureString $CertPlainPassword -AsPlainText -Force
 $PFXCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($CertPath, $CertPassword)
 $Thumbprint = $PFXCert.Thumbprint

 Login-AzureRmAccount -ServicePrincipal -CertificateThumbprint $Thumbprint -ApplicationId $ApplicationId -TenantId $TenantId
```

<span data-ttu-id="e2d15-172">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span><span class="sxs-lookup"><span data-stu-id="e2d15-172">The application ID and tenant ID are not sensitive, so you can embed them directly in your script.</span></span> <span data-ttu-id="e2d15-173">If you need to retrieve the tenant ID, use:</span><span class="sxs-lookup"><span data-stu-id="e2d15-173">If you need to retrieve the tenant ID, use:</span></span>

```powershell
(Get-AzureRmSubscription -SubscriptionName "Contoso Default").TenantId
```

<span data-ttu-id="e2d15-174">If you need to retrieve the application ID, use:</span><span class="sxs-lookup"><span data-stu-id="e2d15-174">If you need to retrieve the application ID, use:</span></span>

```powershell
(Get-AzureRmADApplication -DisplayNameStartWith {display-name}).ApplicationId
```

## <a name="change-credentials"></a><span data-ttu-id="e2d15-175">Change credentials</span><span class="sxs-lookup"><span data-stu-id="e2d15-175">Change credentials</span></span>

<span data-ttu-id="e2d15-176">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use the [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/new-azurermadappcredential) cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e2d15-176">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use the [Remove-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/remove-azurermadappcredential) and [New-AzureRmADAppCredential](/powershell/resourcemanager/azurerm.resources/v3.3.0/new-azurermadappcredential) cmdlets.</span></span>

<span data-ttu-id="e2d15-177">To remove all the credentials for an application, use:</span><span class="sxs-lookup"><span data-stu-id="e2d15-177">To remove all the credentials for an application, use:</span></span>

```powershell
Remove-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -All
```

<span data-ttu-id="e2d15-178">To add a password, use:</span><span class="sxs-lookup"><span data-stu-id="e2d15-178">To add a password, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -Password p@ssword!
```

<span data-ttu-id="e2d15-179">To add a certificate value, create a self-signed certificate as shown in this topic.</span><span class="sxs-lookup"><span data-stu-id="e2d15-179">To add a certificate value, create a self-signed certificate as shown in this topic.</span></span> <span data-ttu-id="e2d15-180">Then, use:</span><span class="sxs-lookup"><span data-stu-id="e2d15-180">Then, use:</span></span>

```powershell
New-AzureRmADAppCredential -ApplicationId 8bc80782-a916-47c8-a47e-4d76ed755275 -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
```

## <a name="save-access-token-to-simplify-log-in"></a><span data-ttu-id="e2d15-181">Save access token to simplify log in</span><span class="sxs-lookup"><span data-stu-id="e2d15-181">Save access token to simplify log in</span></span>
<span data-ttu-id="e2d15-182">To avoid providing the service principal credentials every time it needs to log in, you can save the access token.</span><span class="sxs-lookup"><span data-stu-id="e2d15-182">To avoid providing the service principal credentials every time it needs to log in, you can save the access token.</span></span>

<span data-ttu-id="e2d15-183">To use the current access token in a later session, save the profile.</span><span class="sxs-lookup"><span data-stu-id="e2d15-183">To use the current access token in a later session, save the profile.</span></span>
   
```powershell
Save-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```
   
<span data-ttu-id="e2d15-184">Open the profile and examine its contents.</span><span class="sxs-lookup"><span data-stu-id="e2d15-184">Open the profile and examine its contents.</span></span> <span data-ttu-id="e2d15-185">Notice that it contains an access token.</span><span class="sxs-lookup"><span data-stu-id="e2d15-185">Notice that it contains an access token.</span></span> <span data-ttu-id="e2d15-186">Instead of manually logging in again, simply load the profile.</span><span class="sxs-lookup"><span data-stu-id="e2d15-186">Instead of manually logging in again, simply load the profile.</span></span>
   
```powershell
Select-AzureRmProfile -Path c:\Users\exampleuser\profile\exampleSP.json
```

> [!NOTE]
> The access token expires, so using a saved profile only works for as long as the token is valid.
>  

<span data-ttu-id="e2d15-188">Alternatively, you can invoke REST operations from PowerShell to log in.</span><span class="sxs-lookup"><span data-stu-id="e2d15-188">Alternatively, you can invoke REST operations from PowerShell to log in.</span></span> <span data-ttu-id="e2d15-189">From the authentication response, you can retrieve the access token for use with other operations.</span><span class="sxs-lookup"><span data-stu-id="e2d15-189">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="e2d15-190">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="e2d15-190">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="debug"></a><span data-ttu-id="e2d15-191">Debug</span><span class="sxs-lookup"><span data-stu-id="e2d15-191">Debug</span></span>

<span data-ttu-id="e2d15-192">You may encounter the following errors when creating a service principal:</span><span class="sxs-lookup"><span data-stu-id="e2d15-192">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="e2d15-193">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span><span class="sxs-lookup"><span data-stu-id="e2d15-193">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="e2d15-194">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span><span class="sxs-lookup"><span data-stu-id="e2d15-194">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="e2d15-195">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span><span class="sxs-lookup"><span data-stu-id="e2d15-195">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="e2d15-196">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span><span class="sxs-lookup"><span data-stu-id="e2d15-196">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="e2d15-197">Ask your subscription administrator to add you to User Access Administrator role.</span><span class="sxs-lookup"><span data-stu-id="e2d15-197">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="e2d15-198">Sample applications</span><span class="sxs-lookup"><span data-stu-id="e2d15-198">Sample applications</span></span>
<span data-ttu-id="e2d15-199">The following sample applications show how to log in as the service principal.</span><span class="sxs-lookup"><span data-stu-id="e2d15-199">The following sample applications show how to log in as the service principal.</span></span>

<span data-ttu-id="e2d15-200">**.NET**</span><span class="sxs-lookup"><span data-stu-id="e2d15-200">**.NET**</span></span>

* [<span data-ttu-id="e2d15-201">Deploy an SSH Enabled VM with a Template with .NET</span><span class="sxs-lookup"><span data-stu-id="e2d15-201">Deploy an SSH Enabled VM with a Template with .NET</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-dotnet-template-deployment/)
* [<span data-ttu-id="e2d15-202">Manage Azure resources and resource groups with .NET</span><span class="sxs-lookup"><span data-stu-id="e2d15-202">Manage Azure resources and resource groups with .NET</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-dotnet-resources-and-groups/)

<span data-ttu-id="e2d15-203">**Java**</span><span class="sxs-lookup"><span data-stu-id="e2d15-203">**Java**</span></span>

* [<span data-ttu-id="e2d15-204">Getting Started with Resources - Deploy Using Azure Resource Manager Template - in Java</span><span class="sxs-lookup"><span data-stu-id="e2d15-204">Getting Started with Resources - Deploy Using Azure Resource Manager Template - in Java</span></span>](https://azure.microsoft.com/documentation/samples/resources-java-deploy-using-arm-template/)
* [<span data-ttu-id="e2d15-205">Getting Started with Resources - Manage Resource Group - in Java</span><span class="sxs-lookup"><span data-stu-id="e2d15-205">Getting Started with Resources - Manage Resource Group - in Java</span></span>](https://azure.microsoft.com/documentation/samples/resources-java-manage-resource-group//)

<span data-ttu-id="e2d15-206">**Python**</span><span class="sxs-lookup"><span data-stu-id="e2d15-206">**Python**</span></span>

* [<span data-ttu-id="e2d15-207">Deploy an SSH Enabled VM with a Template in Python</span><span class="sxs-lookup"><span data-stu-id="e2d15-207">Deploy an SSH Enabled VM with a Template in Python</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-python-template-deployment/)
* [<span data-ttu-id="e2d15-208">Managing Azure Resource and Resource Groups with Python</span><span class="sxs-lookup"><span data-stu-id="e2d15-208">Managing Azure Resource and Resource Groups with Python</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-python-resources-and-groups/)

<span data-ttu-id="e2d15-209">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="e2d15-209">**Node.js**</span></span>

* [<span data-ttu-id="e2d15-210">Deploy an SSH Enabled VM with a Template in Node.js</span><span class="sxs-lookup"><span data-stu-id="e2d15-210">Deploy an SSH Enabled VM with a Template in Node.js</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-node-template-deployment/)
* [<span data-ttu-id="e2d15-211">Manage Azure resources and resource groups with Node.js</span><span class="sxs-lookup"><span data-stu-id="e2d15-211">Manage Azure resources and resource groups with Node.js</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-node-resources-and-groups/)

<span data-ttu-id="e2d15-212">**Ruby**</span><span class="sxs-lookup"><span data-stu-id="e2d15-212">**Ruby**</span></span>

* [<span data-ttu-id="e2d15-213">Deploy an SSH Enabled VM with a Template in Ruby</span><span class="sxs-lookup"><span data-stu-id="e2d15-213">Deploy an SSH Enabled VM with a Template in Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-template-deployment/)
* [<span data-ttu-id="e2d15-214">Managing Azure Resource and Resource Groups with Ruby</span><span class="sxs-lookup"><span data-stu-id="e2d15-214">Managing Azure Resource and Resource Groups with Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="e2d15-215">Next Steps</span><span class="sxs-lookup"><span data-stu-id="e2d15-215">Next Steps</span></span>
* <span data-ttu-id="e2d15-216">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e2d15-216">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="e2d15-217">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="e2d15-217">For a more detailed explanation of applications and service principals, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md).</span></span> 
* <span data-ttu-id="e2d15-218">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="e2d15-218">For more information about Azure Active Directory authentication, see [Authentication Scenarios for Azure AD](../active-directory/active-directory-authentication-scenarios.md).</span></span>

