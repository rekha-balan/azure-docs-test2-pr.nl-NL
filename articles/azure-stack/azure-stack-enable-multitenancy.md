---
title: Enable multi-tenancy in Azure Stack | Microsoft Docs
description: Learn how to support multiple Azure AD directories in Azure Stack
services: azure-stack
documentationcenter: ''
author: HeathL17
manager: byronr
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/13/2017
ms.author: helaw
ms.openlocfilehash: cc9d36edceca74ae7fc1c712931bb5929a325443
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552564"
---
# <a name="enable-multi-tenancy-in-azure-stack"></a><span data-ttu-id="fede4-103">Enable multi-tenancy in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fede4-103">Enable multi-tenancy in Azure Stack</span></span>

<span data-ttu-id="fede4-104">You can configure Azure Stack to support users from multiple Azure Active Directory (Azure AD) tenants to use services in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fede4-104">You can configure Azure Stack to support users from multiple Azure Active Directory (Azure AD) tenants to use services in Azure Stack.</span></span> <span data-ttu-id="fede4-105">As an example, consider the following scenario:</span><span class="sxs-lookup"><span data-stu-id="fede4-105">As an example, consider the following scenario:</span></span>

 - <span data-ttu-id="fede4-106">You are the Service Administrator of contoso.onmicrosoft.com, where Azure Stack is installed.</span><span class="sxs-lookup"><span data-stu-id="fede4-106">You are the Service Administrator of contoso.onmicrosoft.com, where Azure Stack is installed.</span></span>
 - <span data-ttu-id="fede4-107">Mary is the Directory Administrator of fabrikam.onmicrosoft.com, where guest users are located.</span><span class="sxs-lookup"><span data-stu-id="fede4-107">Mary is the Directory Administrator of fabrikam.onmicrosoft.com, where guest users are located.</span></span> 
 - <span data-ttu-id="fede4-108">Mary's company receives IaaS and PaaS services from your company, and needs to allow users from the guest directory (fabrikam.onmicrosoft.com) to sign in and use Azure Stack resources in contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="fede4-108">Mary's company receives IaaS and PaaS services from your company, and needs to allow users from the guest directory (fabrikam.onmicrosoft.com) to sign in and use Azure Stack resources in contoso.onmicrosoft.com.</span></span>

<span data-ttu-id="fede4-109">This guide provides the steps required, in the context of this scenario, to configure multi-tenancy in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fede4-109">This guide provides the steps required, in the context of this scenario, to configure multi-tenancy in Azure Stack.</span></span>  <span data-ttu-id="fede4-110">In this scenario, you and Mary must complete steps to enable users from Fabrikam to sign in and consume services from the Azure Stack deployment in Contoso.</span><span class="sxs-lookup"><span data-stu-id="fede4-110">In this scenario, you and Mary must complete steps to enable users from Fabrikam to sign in and consume services from the Azure Stack deployment in Contoso.</span></span>  

## <a name="before-you-begin"></a><span data-ttu-id="fede4-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="fede4-111">Before you begin</span></span>
<span data-ttu-id="fede4-112">There are a few pre-requisites to account for before you configure multi-tenancy in Azure Stack:</span><span class="sxs-lookup"><span data-stu-id="fede4-112">There are a few pre-requisites to account for before you configure multi-tenancy in Azure Stack:</span></span>
  
 - <span data-ttu-id="fede4-113">You and Mary must coordinate administrative steps across both the directory Azure Stack is installed in (Contoso), and the guest directory (Fabrikam).</span><span class="sxs-lookup"><span data-stu-id="fede4-113">You and Mary must coordinate administrative steps across both the directory Azure Stack is installed in (Contoso), and the guest directory (Fabrikam).</span></span>  
 - <span data-ttu-id="fede4-114">Make sure you've [installed](azure-stack-powershell-install.md) and [configured](azure-stack-powershell-configure.md) PowerShell for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fede4-114">Make sure you've [installed](azure-stack-powershell-install.md) and [configured](azure-stack-powershell-configure.md) PowerShell for Azure Stack.</span></span>
 - <span data-ttu-id="fede4-115">[Download the Azure Stack Tools](azure-stack-powershell-download.md), and import the Connect and Identity modules:</span><span class="sxs-lookup"><span data-stu-id="fede4-115">[Download the Azure Stack Tools](azure-stack-powershell-download.md), and import the Connect and Identity modules:</span></span>

    ````PowerShell
        Import-Module .\Connect\AzureStack.Connect.psm1
        Import-Module .\Identity\AzureStack.Identity.psm1
    ```` 
 - <span data-ttu-id="fede4-116">Mary will require [VPN](azure-stack-connect-azure-stack.md#connect-with-vpn) access to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fede4-116">Mary will require [VPN](azure-stack-connect-azure-stack.md#connect-with-vpn) access to Azure Stack.</span></span> 

## <a name="configure-azure-stack-directory"></a><span data-ttu-id="fede4-117">Configure Azure Stack directory</span><span class="sxs-lookup"><span data-stu-id="fede4-117">Configure Azure Stack directory</span></span>
<span data-ttu-id="fede4-118">In this section, you configure Azure Stack to allow sign-ins from Fabrikam Azure AD directory tenants.</span><span class="sxs-lookup"><span data-stu-id="fede4-118">In this section, you configure Azure Stack to allow sign-ins from Fabrikam Azure AD directory tenants.</span></span>

### <a name="create-azure-ad-applications"></a><span data-ttu-id="fede4-119">Create Azure AD applications</span><span class="sxs-lookup"><span data-stu-id="fede4-119">Create Azure AD applications</span></span>
<span data-ttu-id="fede4-120">First, you must publish Azure AD applications to Azure Resource Manager to allow access to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fede4-120">First, you must publish Azure AD applications to Azure Resource Manager to allow access to Azure Stack.</span></span>  <span data-ttu-id="fede4-121">This step only needs to be completed once, regardless of additional guest tenants in the future.</span><span class="sxs-lookup"><span data-stu-id="fede4-121">This step only needs to be completed once, regardless of additional guest tenants in the future.</span></span>  <span data-ttu-id="fede4-122">Run this PowerShell as the Azure Stack Service Administrator from the Azure Stack host or MAS-CON01.</span><span class="sxs-lookup"><span data-stu-id="fede4-122">Run this PowerShell as the Azure Stack Service Administrator from the Azure Stack host or MAS-CON01.</span></span>

````PowerShell 
$adminARMEndpoint = "https://adminmanagement.local.azurestack.external"
    
# Replace the value below with the Azure Stack directory.
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

Publish-AzureStackApplicationsToARM` 
 -AdminResourceManagerEndpoint $adminARMEndpoint`
 -DirectoryTenantName $azureStackDirectoryTenant 
````


### <a name="onboard-guest-directory-tenant"></a><span data-ttu-id="fede4-123">Onboard guest directory tenant</span><span class="sxs-lookup"><span data-stu-id="fede4-123">Onboard guest directory tenant</span></span>
<span data-ttu-id="fede4-124">Next, onboard the Guest Directory Tenant (Fabrikam) to Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fede4-124">Next, onboard the Guest Directory Tenant (Fabrikam) to Azure Stack.</span></span>  <span data-ttu-id="fede4-125">This step configures Azure Resource Manager to accept users and service principals from the guest directory tenant.</span><span class="sxs-lookup"><span data-stu-id="fede4-125">This step configures Azure Resource Manager to accept users and service principals from the guest directory tenant.</span></span>

````PowerShell
$adminARMEndpoint = https://adminmanagement.local.azurestack.external

## Replace the value below with the Azure Stack directory
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

## Replace the value below with the guest tenant directory. 
$guestDirectoryTenantToBeOnboarded = "fabrikam.onmicrosoft.com"

Register-GuestDirectoryTenantToAzureStack -AdminResourceManagerEndpoint $adminARMEndpoint `
 -DirectoryTenantName $azureStackDirectoryTenant`
 -GuestDirectoryTenantName $guestDirectoryTenantToBeOnboarded 
````



## <a name="configure-guest-directory"></a><span data-ttu-id="fede4-126">Configure guest directory</span><span class="sxs-lookup"><span data-stu-id="fede4-126">Configure guest directory</span></span>
<span data-ttu-id="fede4-127">After you complete steps in the Azure Stack directory, Mary must provide consent to Azure Stack accessing the guest directory and register Azure Stack with the guest directory.</span><span class="sxs-lookup"><span data-stu-id="fede4-127">After you complete steps in the Azure Stack directory, Mary must provide consent to Azure Stack accessing the guest directory and register Azure Stack with the guest directory.</span></span> 

### <a name="providing-consent-to-azure-stack"></a><span data-ttu-id="fede4-128">Providing consent to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fede4-128">Providing consent to Azure Stack</span></span>
<span data-ttu-id="fede4-129">The guest directory administrator must provide consent in order for Azure Stack to read information from the guest directory.</span><span class="sxs-lookup"><span data-stu-id="fede4-129">The guest directory administrator must provide consent in order for Azure Stack to read information from the guest directory.</span></span> <span data-ttu-id="fede4-130">The guest administrator opens up a web browser and visits the following URL:  https://portal.local.azurestack.external/guest/signup/< guestDirectoryName >.</span><span class="sxs-lookup"><span data-stu-id="fede4-130">The guest administrator opens up a web browser and visits the following URL:  https://portal.local.azurestack.external/guest/signup/< guestDirectoryName >.</span></span>  <span data-ttu-id="fede4-131">This URL takes the guest directory administrator to an AAD sign-in page where they enter their credentials and click **Accept** on the consent screen.</span><span class="sxs-lookup"><span data-stu-id="fede4-131">This URL takes the guest directory administrator to an AAD sign-in page where they enter their credentials and click **Accept** on the consent screen.</span></span>

<span data-ttu-id="fede4-132">In our example, Mary visits https://portal.azurestack.local/guest/signup/fabrikam.onmicrosoft.com with a web browser.</span><span class="sxs-lookup"><span data-stu-id="fede4-132">In our example, Mary visits https://portal.azurestack.local/guest/signup/fabrikam.onmicrosoft.com with a web browser.</span></span>  

### <a name="registering-azure-stack-with-the-guest-directory"></a><span data-ttu-id="fede4-133">Registering Azure Stack with the guest directory</span><span class="sxs-lookup"><span data-stu-id="fede4-133">Registering Azure Stack with the guest directory</span></span>
<span data-ttu-id="fede4-134">Once the guest directory administrator has provided consent for Azure Stack to access Fabrikam's directory, they must register Azure Stack with Fabrikam's directory tenant.</span><span class="sxs-lookup"><span data-stu-id="fede4-134">Once the guest directory administrator has provided consent for Azure Stack to access Fabrikam's directory, they must register Azure Stack with Fabrikam's directory tenant.</span></span>

````PowerShell
$tenantARMEndpoint = "https://management.local.azurestack.external"
    
## Replace the value below with the guest tenant directory. 
$guestDirectoryTenantName = "fabrikam.onmicrosoft.com"

Register-AzureStackWithMyDirectoryTenant `
 -TenantResourceManagerEndpoint $tenantARMEndpoint `
 -DirectoryTenantName $guestDirectoryTenantName -Verbose 
````
## <a name="direct-users-to-sign-in"></a><span data-ttu-id="fede4-135">Direct users to sign in</span><span class="sxs-lookup"><span data-stu-id="fede4-135">Direct users to sign in</span></span>
<span data-ttu-id="fede4-136">Now that you and Mary have completed the steps to onboard Mary's directory, Mary can direct Fabrikam users to sign in.</span><span class="sxs-lookup"><span data-stu-id="fede4-136">Now that you and Mary have completed the steps to onboard Mary's directory, Mary can direct Fabrikam users to sign in.</span></span>  <span data-ttu-id="fede4-137">Fabrikam users (that is, users with the fabrikam.onmicrosoft.com suffix) sign in by visiting https://portal.local.azurestack.external.</span><span class="sxs-lookup"><span data-stu-id="fede4-137">Fabrikam users (that is, users with the fabrikam.onmicrosoft.com suffix) sign in by visiting https://portal.local.azurestack.external.</span></span>  

<span data-ttu-id="fede4-138">Mary will direct any [foreign principals](../active-directory/active-directory-understanding-resource-access.md) in the Fabrikam directory (that is, users in the Fabrikam directory without the suffix of fabrikam.onmicrosoft.com) to sign in using https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="fede4-138">Mary will direct any [foreign principals](../active-directory/active-directory-understanding-resource-access.md) in the Fabrikam directory (that is, users in the Fabrikam directory without the suffix of fabrikam.onmicrosoft.com) to sign in using https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.</span></span>  <span data-ttu-id="fede4-139">If they do not use this URL, they are sent to their default directory (Fabrikam) and receive an error that says their admin has not consented.</span><span class="sxs-lookup"><span data-stu-id="fede4-139">If they do not use this URL, they are sent to their default directory (Fabrikam) and receive an error that says their admin has not consented.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fede4-140">Next Steps</span><span class="sxs-lookup"><span data-stu-id="fede4-140">Next Steps</span></span>

- [<span data-ttu-id="fede4-141">Manage delegated providers</span><span class="sxs-lookup"><span data-stu-id="fede4-141">Manage delegated providers</span></span>](azure-stack-delegated-provider.md)
- [<span data-ttu-id="fede4-142">Azure Stack key concepts</span><span class="sxs-lookup"><span data-stu-id="fede4-142">Azure Stack key concepts</span></span>](azure-stack-key-features.md)
