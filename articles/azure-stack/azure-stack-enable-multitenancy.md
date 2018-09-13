---
title: Multi-tenancy in Azure Stack
description: Learn how to support multiple Azure Active Directory directories in Azure Stack
services: azure-stack
documentationcenter: ''
author: PatAltimore
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/11/2018
ms.author: patricka
ms.openlocfilehash: 0a10662e359379356ecc8d82af1b7d6331c41a65
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44771660"
---
# <a name="multi-tenancy-in-azure-stack"></a><span data-ttu-id="019ce-103">Multi-tenancy in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="019ce-103">Multi-tenancy in Azure Stack</span></span>

<span data-ttu-id="019ce-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="019ce-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="019ce-105">You can configure Azure Stack to support users from multiple Azure Active Directory (Azure AD) tenants to use services in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="019ce-105">You can configure Azure Stack to support users from multiple Azure Active Directory (Azure AD) tenants to use services in Azure Stack.</span></span> <span data-ttu-id="019ce-106">For example, consider the following scenario:</span><span class="sxs-lookup"><span data-stu-id="019ce-106">For example, consider the following scenario:</span></span>

 - <span data-ttu-id="019ce-107">You are the Service Administrator of contoso.onmicrosoft.com, where Azure Stack is installed.</span><span class="sxs-lookup"><span data-stu-id="019ce-107">You are the Service Administrator of contoso.onmicrosoft.com, where Azure Stack is installed.</span></span>
 - <span data-ttu-id="019ce-108">Mary is the Directory Administrator of fabrikam.onmicrosoft.com, where guest users are located.</span><span class="sxs-lookup"><span data-stu-id="019ce-108">Mary is the Directory Administrator of fabrikam.onmicrosoft.com, where guest users are located.</span></span> 
 - <span data-ttu-id="019ce-109">Mary's company receives IaaS and PaaS services from your company, and needs to allow users from the guest directory (fabrikam.onmicrosoft.com) to sign in and use Azure Stack resources in contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="019ce-109">Mary's company receives IaaS and PaaS services from your company, and needs to allow users from the guest directory (fabrikam.onmicrosoft.com) to sign in and use Azure Stack resources in contoso.onmicrosoft.com.</span></span>

<span data-ttu-id="019ce-110">This guide provides the steps required, in the context of this scenario, to configure multi-tenancy in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="019ce-110">This guide provides the steps required, in the context of this scenario, to configure multi-tenancy in Azure Stack.</span></span> <span data-ttu-id="019ce-111">In this scenario, you and Mary must complete steps to enable users from Fabrikam to sign in and consume services from the Azure Stack deployment in Contoso.</span><span class="sxs-lookup"><span data-stu-id="019ce-111">In this scenario, you and Mary must complete steps to enable users from Fabrikam to sign in and consume services from the Azure Stack deployment in Contoso.</span></span>  

## <a name="enable-multi-tenancy"></a><span data-ttu-id="019ce-112">Enable multi-tenancy</span><span class="sxs-lookup"><span data-stu-id="019ce-112">Enable multi-tenancy</span></span>

<span data-ttu-id="019ce-113">There are a few pre-requisites to account for before you configure multi-tenancy in Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="019ce-113">There are a few pre-requisites to account for before you configure multi-tenancy in Azure Stack:</span></span>
  
 - <span data-ttu-id="019ce-114">You and Mary must coordinate administrative steps across both the directory Azure Stack is installed in (Contoso), and the guest directory (Fabrikam).</span><span class="sxs-lookup"><span data-stu-id="019ce-114">You and Mary must coordinate administrative steps across both the directory Azure Stack is installed in (Contoso), and the guest directory (Fabrikam).</span></span>  
 - <span data-ttu-id="019ce-115">Make sure you've [installed](azure-stack-powershell-install.md) and [configured](azure-stack-powershell-configure-admin.md) PowerShell for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="019ce-115">Make sure you've [installed](azure-stack-powershell-install.md) and [configured](azure-stack-powershell-configure-admin.md) PowerShell for Azure Stack.</span></span>
 - <span data-ttu-id="019ce-116">[Download the Azure Stack Tools](azure-stack-powershell-download.md), and import the Connect and Identity modules:</span><span class="sxs-lookup"><span data-stu-id="019ce-116">[Download the Azure Stack Tools](azure-stack-powershell-download.md), and import the Connect and Identity modules:</span></span>

    ````PowerShell  
    Import-Module .\Connect\AzureStack.Connect.psm1
    Import-Module .\Identity\AzureStack.Identity.psm1
    ````

 - <span data-ttu-id="019ce-117">Mary will require [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) access to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="019ce-117">Mary will require [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) access to Azure Stack.</span></span> 

### <a name="configure-azure-stack-directory"></a><span data-ttu-id="019ce-118">Configure Azure Stack directory</span><span class="sxs-lookup"><span data-stu-id="019ce-118">Configure Azure Stack directory</span></span>

<span data-ttu-id="019ce-119">In this section, you configure Azure Stack to allow sign-ins from Fabrikam Azure AD directory tenants.</span><span class="sxs-lookup"><span data-stu-id="019ce-119">In this section, you configure Azure Stack to allow sign-ins from Fabrikam Azure AD directory tenants.</span></span>

<span data-ttu-id="019ce-120">Onboard the Guest Directory Tenant (Fabrikam) to Azure Stack by configuring Azure Resource Manager to accept users and service principals from the guest directory tenant.</span><span class="sxs-lookup"><span data-stu-id="019ce-120">Onboard the Guest Directory Tenant (Fabrikam) to Azure Stack by configuring Azure Resource Manager to accept users and service principals from the guest directory tenant.</span></span>

````PowerShell  
## The following Azure Resource Manager endpoint is for the ASDK. If you are in a multinode environment, contact your operator or service provider to get the endpoint.
$adminARMEndpoint = "https://adminmanagement.local.azurestack.external"

## Replace the value below with the Azure Stack directory
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

## Replace the value below with the guest tenant directory. 
$guestDirectoryTenantToBeOnboarded = "fabrikam.onmicrosoft.com"

## Replace the value below with the name of the resource group in which the directory tenant registration resource should be created (resource group must already exist).
$ResourceGroupName = "system.local"

## Replace the value below with the region location of the resource group. 
$location = "local"

Register-AzSGuestDirectoryTenant -AdminResourceManagerEndpoint $adminARMEndpoint `
 -DirectoryTenantName $azureStackDirectoryTenant `
 -GuestDirectoryTenantName $guestDirectoryTenantToBeOnboarded `
 -Location $location `
 -ResourceGroupName $ResourceGroupName
````

### <a name="configure-guest-directory"></a><span data-ttu-id="019ce-121">Configure guest directory</span><span class="sxs-lookup"><span data-stu-id="019ce-121">Configure guest directory</span></span>

<span data-ttu-id="019ce-122">After you complete steps in the Azure Stack directory, Mary must provide consent to Azure Stack accessing the guest directory and register Azure Stack with the guest directory.</span><span class="sxs-lookup"><span data-stu-id="019ce-122">After you complete steps in the Azure Stack directory, Mary must provide consent to Azure Stack accessing the guest directory and register Azure Stack with the guest directory.</span></span> 

#### <a name="registering-azure-stack-with-the-guest-directory"></a><span data-ttu-id="019ce-123">Registering Azure Stack with the guest directory</span><span class="sxs-lookup"><span data-stu-id="019ce-123">Registering Azure Stack with the guest directory</span></span>

<span data-ttu-id="019ce-124">Once the guest directory administrator has provided consent for Azure Stack to access Fabrikam's directory, Mary must register Azure Stack with Fabrikam's directory tenant.</span><span class="sxs-lookup"><span data-stu-id="019ce-124">Once the guest directory administrator has provided consent for Azure Stack to access Fabrikam's directory, Mary must register Azure Stack with Fabrikam's directory tenant.</span></span>

````PowerShell
## The following Azure Resource Manager endpoint is for the ASDK. If you are in a multinode environment, contact your operator or service provider to get the endpoint.
$tenantARMEndpoint = "https://management.local.azurestack.external"
    
## Replace the value below with the guest tenant directory. 
$guestDirectoryTenantName = "fabrikam.onmicrosoft.com"

Register-AzSWithMyDirectoryTenant `
 -TenantResourceManagerEndpoint $tenantARMEndpoint `
 -DirectoryTenantName $guestDirectoryTenantName `
 -Verbose 
````

> [!IMPORTANT]
> <span data-ttu-id="019ce-125">If your Azure Stack administrator installs new services or updates in the future, you may need to run this script again.</span><span class="sxs-lookup"><span data-stu-id="019ce-125">If your Azure Stack administrator installs new services or updates in the future, you may need to run this script again.</span></span>
>
> <span data-ttu-id="019ce-126">Run this script again at any time to check the status of the Azure Stack applications in your directory.</span><span class="sxs-lookup"><span data-stu-id="019ce-126">Run this script again at any time to check the status of the Azure Stack applications in your directory.</span></span>


### <a name="activate-the-administrator-and-tenant-portals"></a><span data-ttu-id="019ce-127">Activate the administrator and tenant portals</span><span class="sxs-lookup"><span data-stu-id="019ce-127">Activate the administrator and tenant portals</span></span>
<span data-ttu-id="019ce-128">After deployments that use Azure AD, you must activate both the Azure Stack administrator and tenant portals.</span><span class="sxs-lookup"><span data-stu-id="019ce-128">After deployments that use Azure AD, you must activate both the Azure Stack administrator and tenant portals.</span></span> <span data-ttu-id="019ce-129">This activation consents to giving the Azure Stack portal and Azure Resource Manager the correct permissions (listed on the consent page) for all users of the directory.</span><span class="sxs-lookup"><span data-stu-id="019ce-129">This activation consents to giving the Azure Stack portal and Azure Resource Manager the correct permissions (listed on the consent page) for all users of the directory.</span></span>

- <span data-ttu-id="019ce-130">For the administrator portal, navigate to https://adminportal.local.azurestack.external/guest/signup, read the information, and then click Accept.</span><span class="sxs-lookup"><span data-stu-id="019ce-130">For the administrator portal, navigate to https://adminportal.local.azurestack.external/guest/signup, read the information, and then click Accept.</span></span> <span data-ttu-id="019ce-131">After accepting, you can add service administrators who are not also directory tenant administrators.</span><span class="sxs-lookup"><span data-stu-id="019ce-131">After accepting, you can add service administrators who are not also directory tenant administrators.</span></span>
- <span data-ttu-id="019ce-132">For the tenant portal, navigate to https://portal.local.azurestack.external/guest/signup, read the information, and then click Accept.</span><span class="sxs-lookup"><span data-stu-id="019ce-132">For the tenant portal, navigate to https://portal.local.azurestack.external/guest/signup, read the information, and then click Accept.</span></span> <span data-ttu-id="019ce-133">After accepting, users in the directory can sign in to the tenant portal.</span><span class="sxs-lookup"><span data-stu-id="019ce-133">After accepting, users in the directory can sign in to the tenant portal.</span></span> 
 
> [!NOTE] 
> <span data-ttu-id="019ce-134">If the portals are not activated, only the directory administrator can sign in and use the portals.</span><span class="sxs-lookup"><span data-stu-id="019ce-134">If the portals are not activated, only the directory administrator can sign in and use the portals.</span></span> <span data-ttu-id="019ce-135">If another user signs in, they will see an error that tells them that the administrator has not granted permissions to other users.</span><span class="sxs-lookup"><span data-stu-id="019ce-135">If another user signs in, they will see an error that tells them that the administrator has not granted permissions to other users.</span></span> <span data-ttu-id="019ce-136">When the administrator does not natively belong to the directory Azure Stack is registered to, the Azure Stack directory must be appended to the activation URL.</span><span class="sxs-lookup"><span data-stu-id="019ce-136">When the administrator does not natively belong to the directory Azure Stack is registered to, the Azure Stack directory must be appended to the activation URL.</span></span> <span data-ttu-id="019ce-137">For example, if Azure Stack is registered to fabrikam.onmicrosoft.com and the admin user is admin@contoso.com, navigate to https://portal.local.azurestack.external/guest/signup/fabrikam.onmicrosoft.com to activate the portal.</span><span class="sxs-lookup"><span data-stu-id="019ce-137">For example, if Azure Stack is registered to fabrikam.onmicrosoft.com and the admin user is admin@contoso.com, navigate to https://portal.local.azurestack.external/guest/signup/fabrikam.onmicrosoft.com to activate the portal.</span></span>



### <a name="direct-users-to-sign-in"></a><span data-ttu-id="019ce-138">Direct users to sign in</span><span class="sxs-lookup"><span data-stu-id="019ce-138">Direct users to sign in</span></span>

<span data-ttu-id="019ce-139">Now that you and Mary have completed the steps to onboard Mary's directory, Mary can direct Fabrikam users to sign in.</span><span class="sxs-lookup"><span data-stu-id="019ce-139">Now that you and Mary have completed the steps to onboard Mary's directory, Mary can direct Fabrikam users to sign in.</span></span>  <span data-ttu-id="019ce-140">Fabrikam users (that is, users with the fabrikam.onmicrosoft.com suffix) sign in by visiting https://portal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="019ce-140">Fabrikam users (that is, users with the fabrikam.onmicrosoft.com suffix) sign in by visiting https://portal.local.azurestack.external.</span></span>  

<span data-ttu-id="019ce-141">Mary will direct any [foreign principals](../role-based-access-control/rbac-and-directory-admin-roles.md) in the Fabrikam directory (that is, users in the Fabrikam directory without the suffix of fabrikam.onmicrosoft.com) to sign in using https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="019ce-141">Mary will direct any [foreign principals](../role-based-access-control/rbac-and-directory-admin-roles.md) in the Fabrikam directory (that is, users in the Fabrikam directory without the suffix of fabrikam.onmicrosoft.com) to sign in using https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.</span></span>  <span data-ttu-id="019ce-142">If they do not use this URL, they are sent to their default directory (Fabrikam) and receive an error that says their admin has not consented.</span><span class="sxs-lookup"><span data-stu-id="019ce-142">If they do not use this URL, they are sent to their default directory (Fabrikam) and receive an error that says their admin has not consented.</span></span>

## <a name="disable-multi-tenancy"></a><span data-ttu-id="019ce-143">Disable multi-tenancy</span><span class="sxs-lookup"><span data-stu-id="019ce-143">Disable multi-tenancy</span></span>

<span data-ttu-id="019ce-144">If you no longer want multiple tenants in Azure Stack, you can disable multi-tenancy by doing the following steps in order:</span><span class="sxs-lookup"><span data-stu-id="019ce-144">If you no longer want multiple tenants in Azure Stack, you can disable multi-tenancy by doing the following steps in order:</span></span>

1. <span data-ttu-id="019ce-145">As the administrator of the guest directory (Mary in this scenario), run *Unregister-AzsWithMyDirectoryTenant*.</span><span class="sxs-lookup"><span data-stu-id="019ce-145">As the administrator of the guest directory (Mary in this scenario), run *Unregister-AzsWithMyDirectoryTenant*.</span></span> <span data-ttu-id="019ce-146">The cmdlet uninstalls all the Azure Stack applications from the new directory.</span><span class="sxs-lookup"><span data-stu-id="019ce-146">The cmdlet uninstalls all the Azure Stack applications from the new directory.</span></span>

    ``` PowerShell
    ## The following Azure Resource Manager endpoint is for the ASDK. If you are in a multinode environment, contact your operator or service provider to get the endpoint.
    $tenantARMEndpoint = "https://management.local.azurestack.external"
        
    ## Replace the value below with the guest tenant directory. 
    $guestDirectoryTenantName = "fabrikam.onmicrosoft.com"
    
    Unregister-AzsWithMyDirectoryTenant `
     -TenantResourceManagerEndpoint $tenantARMEndpoint `
     -DirectoryTenantName $guestDirectoryTenantName `
     -Verbose 
    ```

2. <span data-ttu-id="019ce-147">As the service administrator of Azure Stack (you in this scenario), run *Unregister-AzSGuestDirectoryTenant*.</span><span class="sxs-lookup"><span data-stu-id="019ce-147">As the service administrator of Azure Stack (you in this scenario), run *Unregister-AzSGuestDirectoryTenant*.</span></span> 

    ``` PowerShell  
    ## The following Azure Resource Manaager endpoint is for the ASDK. If you are in a multinode environment, contact your operator or service provider to get the endpoint.
    $adminARMEndpoint = "https://adminmanagement.local.azurestack.external"
    
    ## Replace the value below with the Azure Stack directory
    $azureStackDirectoryTenant = "contoso.onmicrosoft.com"
    
    ## Replace the value below with the guest tenant directory. 
    $guestDirectoryTenantToBeDecommissioned = "fabrikam.onmicrosoft.com"
    
    ## Replace the value below with the name of the resource group in which the directory tenant registration resource should be created (resource group must already exist).
    $ResourceGroupName = "system.local"
    
    Unregister-AzSGuestDirectoryTenant -AdminResourceManagerEndpoint $adminARMEndpoint `
     -DirectoryTenantName $azureStackDirectoryTenant `
     -GuestDirectoryTenantName $guestDirectoryTenantToBeDecommissioned `
     -ResourceGroupName $ResourceGroupName
    ```

    > [!WARNING]
    > <span data-ttu-id="019ce-148">The disable multi-tenancy steps must be performed in order.</span><span class="sxs-lookup"><span data-stu-id="019ce-148">The disable multi-tenancy steps must be performed in order.</span></span> <span data-ttu-id="019ce-149">Step #1 fails if step #2 is completed first.</span><span class="sxs-lookup"><span data-stu-id="019ce-149">Step #1 fails if step #2 is completed first.</span></span>

## <a name="next-steps"></a><span data-ttu-id="019ce-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="019ce-150">Next steps</span></span>

- [<span data-ttu-id="019ce-151">Manage delegated providers</span><span class="sxs-lookup"><span data-stu-id="019ce-151">Manage delegated providers</span></span>](azure-stack-delegated-provider.md)
- [<span data-ttu-id="019ce-152">Azure Stack key concepts</span><span class="sxs-lookup"><span data-stu-id="019ce-152">Azure Stack key concepts</span></span>](azure-stack-key-features.md)
