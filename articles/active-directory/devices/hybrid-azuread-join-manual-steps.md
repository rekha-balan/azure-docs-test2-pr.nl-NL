---
title: Configure hybrid Azure Active Directory joined devices manually | Microsoft Docs
description: Learn how to  manually configure hybrid Azure Active Directory joined devices.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.component: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 08/25/2018
ms.author: markvi
ms.reviewer: sandeo
ms.openlocfilehash: 4155ea7c24746f9d3381f2d1e4a1e08a7a56206a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871090"
---
# <a name="tutorial-configure-hybrid-azure-active-directory-joined-devices-manually"></a><span data-ttu-id="407d2-103">Tutorial: Configure hybrid Azure Active Directory joined devices manually</span><span class="sxs-lookup"><span data-stu-id="407d2-103">Tutorial: Configure hybrid Azure Active Directory joined devices manually</span></span> 

<span data-ttu-id="407d2-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span><span class="sxs-lookup"><span data-stu-id="407d2-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> <span data-ttu-id="407d2-105">For more details, see the [Introduction to device management in Azure Active Directory](overview.md).</span><span class="sxs-lookup"><span data-stu-id="407d2-105">For more details, see the [Introduction to device management in Azure Active Directory](overview.md).</span></span>


> [!TIP]
> <span data-ttu-id="407d2-106">If using Azure AD Connect is an option for you, see [Select your scenario](hybrid-azuread-join-plan.md#select-your-scenario).</span><span class="sxs-lookup"><span data-stu-id="407d2-106">If using Azure AD Connect is an option for you, see [Select your scenario](hybrid-azuread-join-plan.md#select-your-scenario).</span></span> <span data-ttu-id="407d2-107">By using Azure AD Connect, you can simplify the configuration of hybrid Azure AD join significantly.</span><span class="sxs-lookup"><span data-stu-id="407d2-107">By using Azure AD Connect, you can simplify the configuration of hybrid Azure AD join significantly.</span></span>



<span data-ttu-id="407d2-108">If you have an on-premises Active Directory environment and you want to join your domain-joined devices to Azure AD, you can accomplish this by configuring hybrid Azure AD joined devices.</span><span class="sxs-lookup"><span data-stu-id="407d2-108">If you have an on-premises Active Directory environment and you want to join your domain-joined devices to Azure AD, you can accomplish this by configuring hybrid Azure AD joined devices.</span></span> <span data-ttu-id="407d2-109">In this tutorial, you learn how to manually configure hybrid Azure AD join for your devices.</span><span class="sxs-lookup"><span data-stu-id="407d2-109">In this tutorial, you learn how to manually configure hybrid Azure AD join for your devices.</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="407d2-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="407d2-110">Prerequisites</span></span>
> * <span data-ttu-id="407d2-111">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="407d2-111">Configuration steps</span></span>
> * <span data-ttu-id="407d2-112">Configure service connection point</span><span class="sxs-lookup"><span data-stu-id="407d2-112">Configure service connection point</span></span>
> * <span data-ttu-id="407d2-113">Setup issuance of claims</span><span class="sxs-lookup"><span data-stu-id="407d2-113">Setup issuance of claims</span></span>
> * <span data-ttu-id="407d2-114">Enable Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="407d2-114">Enable Windows down-level devices</span></span>
> * <span data-ttu-id="407d2-115">Verify joined devices</span><span class="sxs-lookup"><span data-stu-id="407d2-115">Verify joined devices</span></span>
> * <span data-ttu-id="407d2-116">Troubleshoot your implementation</span><span class="sxs-lookup"><span data-stu-id="407d2-116">Troubleshoot your implementation</span></span>
 




## <a name="prerequisites"></a><span data-ttu-id="407d2-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="407d2-117">Prerequisites</span></span>

<span data-ttu-id="407d2-118">This tutorial assumes that you are familiar with:</span><span class="sxs-lookup"><span data-stu-id="407d2-118">This tutorial assumes that you are familiar with:</span></span>
    
-  [<span data-ttu-id="407d2-119">Introduction to device management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="407d2-119">Introduction to device management in Azure Active Directory</span></span>](../device-management-introduction.md)
    
-  [<span data-ttu-id="407d2-120">How to plan your hybrid Azure Active Directory join implementation</span><span class="sxs-lookup"><span data-stu-id="407d2-120">How to plan your hybrid Azure Active Directory join implementation</span></span>](hybrid-azuread-join-plan.md)

-  [<span data-ttu-id="407d2-121">How to control the hybrid Azure AD join of your devices</span><span class="sxs-lookup"><span data-stu-id="407d2-121">How to control the hybrid Azure AD join of your devices</span></span>](hybrid-azuread-join-control.md)


<span data-ttu-id="407d2-122">Before you start enabling hybrid Azure AD joined devices in your organization, you need to make sure that:</span><span class="sxs-lookup"><span data-stu-id="407d2-122">Before you start enabling hybrid Azure AD joined devices in your organization, you need to make sure that:</span></span>

- <span data-ttu-id="407d2-123">You are running an up-to-date version of Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="407d2-123">You are running an up-to-date version of Azure AD connect.</span></span>

- <span data-ttu-id="407d2-124">Azure AD connect has synchronized the computer objects of the devices you want to be hybrid Azure AD joined to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="407d2-124">Azure AD connect has synchronized the computer objects of the devices you want to be hybrid Azure AD joined to Azure AD.</span></span> <span data-ttu-id="407d2-125">If the computer objects belong to specific organizational units (OU), then these OUs need to be configured for synchronization in Azure AD connect as well.</span><span class="sxs-lookup"><span data-stu-id="407d2-125">If the computer objects belong to specific organizational units (OU), then these OUs need to be configured for synchronization in Azure AD connect as well.</span></span>

  

<span data-ttu-id="407d2-126">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="407d2-126">Azure AD Connect:</span></span>

- <span data-ttu-id="407d2-127">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="407d2-127">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="407d2-128">Enables other device related features like Windows Hello for Business.</span><span class="sxs-lookup"><span data-stu-id="407d2-128">Enables other device related features like Windows Hello for Business.</span></span>

<span data-ttu-id="407d2-129">Make sure that the following URLs are accessible from computers inside your organization network for registration of computers to Azure AD:</span><span class="sxs-lookup"><span data-stu-id="407d2-129">Make sure that the following URLs are accessible from computers inside your organization network for registration of computers to Azure AD:</span></span>

- https://enterpriseregistration.windows.net

- <span data-ttu-id="407d2-130">https://login.microsoftonline.com Allow</span><span class="sxs-lookup"><span data-stu-id="407d2-130">https://login.microsoftonline.com Allow</span></span>
- https://device.login.microsoftonline.com

- <span data-ttu-id="407d2-131">Your organization's STS (federated domains)</span><span class="sxs-lookup"><span data-stu-id="407d2-131">Your organization's STS (federated domains)</span></span>

<span data-ttu-id="407d2-132">If not already done, your organization's STS (for federated domains) should be included in the user's local intranet settings.</span><span class="sxs-lookup"><span data-stu-id="407d2-132">If not already done, your organization's STS (for federated domains) should be included in the user's local intranet settings.</span></span>

<span data-ttu-id="407d2-133">If your organization is planning to use Seamless SSO, then the following URLs need to be reachable from the computers inside your organization and they must also be added to the user's local intranet zone:</span><span class="sxs-lookup"><span data-stu-id="407d2-133">If your organization is planning to use Seamless SSO, then the following URLs need to be reachable from the computers inside your organization and they must also be added to the user's local intranet zone:</span></span>

- https://autologon.microsoftazuread-sso.com

- <span data-ttu-id="407d2-134">Also, the following setting should be enabled in the user's intranet zone: "Allow status bar updates via script."</span><span class="sxs-lookup"><span data-stu-id="407d2-134">Also, the following setting should be enabled in the user's intranet zone: "Allow status bar updates via script."</span></span>

<span data-ttu-id="407d2-135">If your organization uses managed (non-federated) setup with on-premises AD and does not use ADFS to federate with Azure AD, then hybrid Azure AD join on Windows 10 relies on the computer objects in AD to be sync'ed to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="407d2-135">If your organization uses managed (non-federated) setup with on-premises AD and does not use ADFS to federate with Azure AD, then hybrid Azure AD join on Windows 10 relies on the computer objects in AD to be sync'ed to Azure AD.</span></span> <span data-ttu-id="407d2-136">Make sure that any Organizational Units (OU) that contain the computer objects that need to be hybrid Azure AD joined are enabled for sync in the Azure AD Connect sync configuration.</span><span class="sxs-lookup"><span data-stu-id="407d2-136">Make sure that any Organizational Units (OU) that contain the computer objects that need to be hybrid Azure AD joined are enabled for sync in the Azure AD Connect sync configuration.</span></span>

<span data-ttu-id="407d2-137">For Windows 10 devices on version 1703 or earlier, if your organization requires access to the Internet via an outbound proxy, you must implement Web Proxy Auto-Discovery (WPAD) to enable Windows 10 computers to register to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="407d2-137">For Windows 10 devices on version 1703 or earlier, if your organization requires access to the Internet via an outbound proxy, you must implement Web Proxy Auto-Discovery (WPAD) to enable Windows 10 computers to register to Azure AD.</span></span> 

## <a name="configuration-steps"></a><span data-ttu-id="407d2-138">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="407d2-138">Configuration steps</span></span>

<span data-ttu-id="407d2-139">You can configure hybrid Azure AD joined devices for various types of Windows device platforms.</span><span class="sxs-lookup"><span data-stu-id="407d2-139">You can configure hybrid Azure AD joined devices for various types of Windows device platforms.</span></span> <span data-ttu-id="407d2-140">This topic includes the required steps for all typical configuration scenarios.</span><span class="sxs-lookup"><span data-stu-id="407d2-140">This topic includes the required steps for all typical configuration scenarios.</span></span>  

<span data-ttu-id="407d2-141">Use the following table to get an overview of the steps that are required for your scenario:</span><span class="sxs-lookup"><span data-stu-id="407d2-141">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="407d2-142">Steps</span><span class="sxs-lookup"><span data-stu-id="407d2-142">Steps</span></span>                                      | <span data-ttu-id="407d2-143">Windows current and password hash sync</span><span class="sxs-lookup"><span data-stu-id="407d2-143">Windows current and password hash sync</span></span> | <span data-ttu-id="407d2-144">Windows current and federation</span><span class="sxs-lookup"><span data-stu-id="407d2-144">Windows current and federation</span></span> | <span data-ttu-id="407d2-145">Windows down-level</span><span class="sxs-lookup"><span data-stu-id="407d2-145">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="407d2-146">Configure service connection point</span><span class="sxs-lookup"><span data-stu-id="407d2-146">Configure service connection point</span></span> | ![Check][1]                            | ![Check][1]                    | ![Check][1]        |
| <span data-ttu-id="407d2-150">Setup issuance of claims</span><span class="sxs-lookup"><span data-stu-id="407d2-150">Setup issuance of claims</span></span>           |                                        | ![Check][1]                    | ![Check][1]        |
| <span data-ttu-id="407d2-153">Enable non-Windows 10 devices</span><span class="sxs-lookup"><span data-stu-id="407d2-153">Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Check][1]        |
| <span data-ttu-id="407d2-155">Verify joined devices</span><span class="sxs-lookup"><span data-stu-id="407d2-155">Verify joined devices</span></span>          | ![Check][1]                            | ![Check][1]                    | ![Check][1]        |



## <a name="configure-service-connection-point"></a><span data-ttu-id="407d2-159">Configure service connection point</span><span class="sxs-lookup"><span data-stu-id="407d2-159">Configure service connection point</span></span>

<span data-ttu-id="407d2-160">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span><span class="sxs-lookup"><span data-stu-id="407d2-160">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="407d2-161">In your on-premises Active Directory (AD), the SCP object for the hybrid Azure AD joined devices must exist in the configuration naming context partition of the computer's forest.</span><span class="sxs-lookup"><span data-stu-id="407d2-161">In your on-premises Active Directory (AD), the SCP object for the hybrid Azure AD joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="407d2-162">There is only one configuration naming context per forest.</span><span class="sxs-lookup"><span data-stu-id="407d2-162">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="407d2-163">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span><span class="sxs-lookup"><span data-stu-id="407d2-163">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="407d2-164">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span><span class="sxs-lookup"><span data-stu-id="407d2-164">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="407d2-165">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span><span class="sxs-lookup"><span data-stu-id="407d2-165">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="407d2-166">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span><span class="sxs-lookup"><span data-stu-id="407d2-166">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="407d2-167">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span><span class="sxs-lookup"><span data-stu-id="407d2-167">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="407d2-168">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="407d2-168">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="407d2-169">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span><span class="sxs-lookup"><span data-stu-id="407d2-169">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="407d2-170">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span><span class="sxs-lookup"><span data-stu-id="407d2-170">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="407d2-171">Enterprise admin credential is required to run this cmdlet.</span><span class="sxs-lookup"><span data-stu-id="407d2-171">Enterprise admin credential is required to run this cmdlet.</span></span>  
<span data-ttu-id="407d2-172">The cmdlet:</span><span class="sxs-lookup"><span data-stu-id="407d2-172">The cmdlet:</span></span>

- <span data-ttu-id="407d2-173">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span><span class="sxs-lookup"><span data-stu-id="407d2-173">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="407d2-174">Requires you to specify the `AdConnectorAccount` parameter.</span><span class="sxs-lookup"><span data-stu-id="407d2-174">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="407d2-175">This is the account that is configured as Active Directory connector account in Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="407d2-175">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="407d2-176">The following script shows an example for using the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="407d2-176">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="407d2-177">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span><span class="sxs-lookup"><span data-stu-id="407d2-177">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="407d2-178">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="407d2-178">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="407d2-179">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="407d2-179">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="407d2-180">Uses the Active Directory PowerShell module and AD DS Tools, which rely on Active Directory Web Services running on a domain controller.</span><span class="sxs-lookup"><span data-stu-id="407d2-180">Uses the Active Directory PowerShell module and AD DS Tools, which rely on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="407d2-181">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span><span class="sxs-lookup"><span data-stu-id="407d2-181">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="407d2-182">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="407d2-182">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="407d2-183">To download this module, use this [link](https://msconfiggallery.cloudapp.net/packages/MSOnline/1.1.166.0/).</span><span class="sxs-lookup"><span data-stu-id="407d2-183">To download this module, use this [link](https://msconfiggallery.cloudapp.net/packages/MSOnline/1.1.166.0/).</span></span>   
- <span data-ttu-id="407d2-184">If the AD DS tools are not installed, the `Initialize-ADSyncDomainJoinedComputerSync` will fail.</span><span class="sxs-lookup"><span data-stu-id="407d2-184">If the AD DS tools are not installed, the `Initialize-ADSyncDomainJoinedComputerSync` will fail.</span></span>  <span data-ttu-id="407d2-185">The AD DS tools can be installed through Server Manager under Features - Remote Server Administration Tools - Role Administration Tools.</span><span class="sxs-lookup"><span data-stu-id="407d2-185">The AD DS tools can be installed through Server Manager under Features - Remote Server Administration Tools - Role Administration Tools.</span></span>

<span data-ttu-id="407d2-186">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span><span class="sxs-lookup"><span data-stu-id="407d2-186">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="407d2-187">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span><span class="sxs-lookup"><span data-stu-id="407d2-187">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC
    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()

<span data-ttu-id="407d2-188">In the script above,</span><span class="sxs-lookup"><span data-stu-id="407d2-188">In the script above,</span></span>

- <span data-ttu-id="407d2-189">`$verifiedDomain = "contoso.com"` is a placeholder you need to replace with one of your verified domain names in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="407d2-189">`$verifiedDomain = "contoso.com"` is a placeholder you need to replace with one of your verified domain names in Azure AD.</span></span> <span data-ttu-id="407d2-190">You will have to own the domain before you can use it.</span><span class="sxs-lookup"><span data-stu-id="407d2-190">You will have to own the domain before you can use it.</span></span>

<span data-ttu-id="407d2-191">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](../active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="407d2-191">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](../active-directory-domains-add-azure-portal.md).</span></span>  
<span data-ttu-id="407d2-192">To get a list of your verified company domains, you can use the [Get-AzureADDomain](/powershell/module/Azuread/Get-AzureADDomain?view=azureadps-2.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="407d2-192">To get a list of your verified company domains, you can use the [Get-AzureADDomain](/powershell/module/Azuread/Get-AzureADDomain?view=azureadps-2.0) cmdlet.</span></span> 

![Get-AzureADDomain](./media/hybrid-azuread-join-manual-steps/01.png)

## <a name="setup-issuance-of-claims"></a><span data-ttu-id="407d2-194">Setup issuance of claims</span><span class="sxs-lookup"><span data-stu-id="407d2-194">Setup issuance of claims</span></span>

<span data-ttu-id="407d2-195">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="407d2-195">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="407d2-196">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="407d2-196">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="407d2-197">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span><span class="sxs-lookup"><span data-stu-id="407d2-197">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="407d2-198">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span><span class="sxs-lookup"><span data-stu-id="407d2-198">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="407d2-199">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span><span class="sxs-lookup"><span data-stu-id="407d2-199">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="407d2-200">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="407d2-200">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="407d2-201">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span><span class="sxs-lookup"><span data-stu-id="407d2-201">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="407d2-202">The following claims must exist in the token received by Azure DRS for device registration to complete.</span><span class="sxs-lookup"><span data-stu-id="407d2-202">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="407d2-203">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span><span class="sxs-lookup"><span data-stu-id="407d2-203">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="407d2-204">If you have more than one verified domain name, you need to provide the following claim for computers:</span><span class="sxs-lookup"><span data-stu-id="407d2-204">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="407d2-205">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span><span class="sxs-lookup"><span data-stu-id="407d2-205">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="407d2-206">In the following sections, you find information about:</span><span class="sxs-lookup"><span data-stu-id="407d2-206">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="407d2-207">The values each claim should have</span><span class="sxs-lookup"><span data-stu-id="407d2-207">The values each claim should have</span></span>
- <span data-ttu-id="407d2-208">How a definition would look like in AD FS</span><span class="sxs-lookup"><span data-stu-id="407d2-208">How a definition would look like in AD FS</span></span>

<span data-ttu-id="407d2-209">The definition helps you to verify whether the values are present or if you need to create them.</span><span class="sxs-lookup"><span data-stu-id="407d2-209">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="407d2-210">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span><span class="sxs-lookup"><span data-stu-id="407d2-210">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="407d2-211">Issue account type claim</span><span class="sxs-lookup"><span data-stu-id="407d2-211">Issue account type claim</span></span>

<span data-ttu-id="407d2-212">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span><span class="sxs-lookup"><span data-stu-id="407d2-212">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="407d2-213">In AD FS, you can add an issuance transform rule that looks like this:</span><span class="sxs-lookup"><span data-stu-id="407d2-213">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="407d2-214">Issue objectGUID of the computer account on-premises</span><span class="sxs-lookup"><span data-stu-id="407d2-214">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="407d2-215">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span><span class="sxs-lookup"><span data-stu-id="407d2-215">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="407d2-216">In AD FS, you can add an issuance transform rule that looks like this:</span><span class="sxs-lookup"><span data-stu-id="407d2-216">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="407d2-217">Issue objectSID of the computer account on-premises</span><span class="sxs-lookup"><span data-stu-id="407d2-217">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="407d2-218">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the **objectSid** value of the on-premises computer account.</span><span class="sxs-lookup"><span data-stu-id="407d2-218">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="407d2-219">In AD FS, you can add an issuance transform rule that looks like this:</span><span class="sxs-lookup"><span data-stu-id="407d2-219">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="407d2-220">Issue issuerID for computer when multiple verified domain names in Azure AD</span><span class="sxs-lookup"><span data-stu-id="407d2-220">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="407d2-221">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span><span class="sxs-lookup"><span data-stu-id="407d2-221">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="407d2-222">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span><span class="sxs-lookup"><span data-stu-id="407d2-222">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="407d2-223">Please note that one rule to explicitly issue the rule for users is necessary.</span><span class="sxs-lookup"><span data-stu-id="407d2-223">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="407d2-224">In the rules below, a first rule identifying user vs. computer authentication is added.</span><span class="sxs-lookup"><span data-stu-id="407d2-224">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with the value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


<span data-ttu-id="407d2-225">In the claim above,</span><span class="sxs-lookup"><span data-stu-id="407d2-225">In the claim above,</span></span>

- <span data-ttu-id="407d2-226">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="407d2-226">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD.</span></span> <span data-ttu-id="407d2-227">For example, Value = "http://contoso.com/adfs/services/trust/"</span><span class="sxs-lookup"><span data-stu-id="407d2-227">For example, Value = "http://contoso.com/adfs/services/trust/"</span></span>



<span data-ttu-id="407d2-228">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](../active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="407d2-228">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](../active-directory-domains-add-azure-portal.md).</span></span>  

<span data-ttu-id="407d2-229">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="407d2-229">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/hybrid-azuread-join-manual-steps/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="407d2-231">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span><span class="sxs-lookup"><span data-stu-id="407d2-231">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="407d2-232">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span><span class="sxs-lookup"><span data-stu-id="407d2-232">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="407d2-233">In AD FS, you can create an issuance transform rule as follows:</span><span class="sxs-lookup"><span data-stu-id="407d2-233">In AD FS, you can create an issuance transform rule as follows:</span></span>

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="407d2-234">Helper script to create the AD FS issuance transform rules</span><span class="sxs-lookup"><span data-stu-id="407d2-234">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="407d2-235">The following script helps you with the creation of the issuance transform rules described above.</span><span class="sxs-lookup"><span data-stu-id="407d2-235">The following script helps you with the creation of the issuance transform rules described above.</span></span>

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with the value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a><span data-ttu-id="407d2-236">Remarks</span><span class="sxs-lookup"><span data-stu-id="407d2-236">Remarks</span></span> 

- <span data-ttu-id="407d2-237">This script appends the rules to the existing rules.</span><span class="sxs-lookup"><span data-stu-id="407d2-237">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="407d2-238">Do not run the script twice because the set of rules would be added twice.</span><span class="sxs-lookup"><span data-stu-id="407d2-238">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="407d2-239">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span><span class="sxs-lookup"><span data-stu-id="407d2-239">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="407d2-240">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span><span class="sxs-lookup"><span data-stu-id="407d2-240">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="407d2-241">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span><span class="sxs-lookup"><span data-stu-id="407d2-241">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="407d2-242">Here is an example for this rule:</span><span class="sxs-lookup"><span data-stu-id="407d2-242">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="407d2-243">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span><span class="sxs-lookup"><span data-stu-id="407d2-243">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span></span>

## <a name="enable-windows-down-level-devices"></a><span data-ttu-id="407d2-244">Enable Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="407d2-244">Enable Windows down-level devices</span></span>

<span data-ttu-id="407d2-245">If some of your domain-joined devices are Windows down-level devices, you need to:</span><span class="sxs-lookup"><span data-stu-id="407d2-245">If some of your domain-joined devices are Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="407d2-246">Set a policy in Azure AD to enable users to register devices.</span><span class="sxs-lookup"><span data-stu-id="407d2-246">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="407d2-247">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span><span class="sxs-lookup"><span data-stu-id="407d2-247">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="407d2-248">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span><span class="sxs-lookup"><span data-stu-id="407d2-248">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="407d2-249">Set policy in Azure AD to enable users to register devices</span><span class="sxs-lookup"><span data-stu-id="407d2-249">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="407d2-250">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span><span class="sxs-lookup"><span data-stu-id="407d2-250">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="407d2-251">In the Azure portal, you can find this setting under:</span><span class="sxs-lookup"><span data-stu-id="407d2-251">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="407d2-252">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span><span class="sxs-lookup"><span data-stu-id="407d2-252">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Register devices](./media/hybrid-azuread-join-manual-steps/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="407d2-254">Configure on-premises federation service</span><span class="sxs-lookup"><span data-stu-id="407d2-254">Configure on-premises federation service</span></span> 

<span data-ttu-id="407d2-255">Your on-premises federation service must support issuing the **authenticationmethod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span><span class="sxs-lookup"><span data-stu-id="407d2-255">Your on-premises federation service must support issuing the **authenticationmethod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="407d2-256">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span><span class="sxs-lookup"><span data-stu-id="407d2-256">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="407d2-257">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span><span class="sxs-lookup"><span data-stu-id="407d2-257">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="407d2-258">**To add this rule:**</span><span class="sxs-lookup"><span data-stu-id="407d2-258">**To add this rule:**</span></span>

1. <span data-ttu-id="407d2-259">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="407d2-259">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="407d2-260">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span><span class="sxs-lookup"><span data-stu-id="407d2-260">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="407d2-261">On the **Issuance Transform Rules** tab, select **Add Rule**.</span><span class="sxs-lookup"><span data-stu-id="407d2-261">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="407d2-262">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span><span class="sxs-lookup"><span data-stu-id="407d2-262">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="407d2-263">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="407d2-263">Select **Next**.</span></span>
6. <span data-ttu-id="407d2-264">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span><span class="sxs-lookup"><span data-stu-id="407d2-264">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="407d2-265">In the **Claim rule** box, type the following rule:</span><span class="sxs-lookup"><span data-stu-id="407d2-265">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="407d2-266">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span><span class="sxs-lookup"><span data-stu-id="407d2-266">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="407d2-267">This object usually is named **Microsoft Office 365 Identity Platform**.</span><span class="sxs-lookup"><span data-stu-id="407d2-267">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="407d2-268">Add the Azure AD device authentication end-point to the Local Intranet zones</span><span class="sxs-lookup"><span data-stu-id="407d2-268">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="407d2-269">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="407d2-269">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`


## <a name="verify-joined-devices"></a><span data-ttu-id="407d2-270">Verify joined devices</span><span class="sxs-lookup"><span data-stu-id="407d2-270">Verify joined devices</span></span>

<span data-ttu-id="407d2-271">You can check successful joined devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="407d2-271">You can check successful joined devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="407d2-272">The output of this cmdlet shows devices that are registered and joined with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="407d2-272">The output of this cmdlet shows devices that are registered and joined with Azure AD.</span></span> <span data-ttu-id="407d2-273">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span><span class="sxs-lookup"><span data-stu-id="407d2-273">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="407d2-274">Domain joined devices have a value of **Domain Joined**.</span><span class="sxs-lookup"><span data-stu-id="407d2-274">Domain joined devices have a value of **Domain Joined**.</span></span>



## <a name="troubleshoot-your-implementation"></a><span data-ttu-id="407d2-275">Troubleshoot your implementation</span><span class="sxs-lookup"><span data-stu-id="407d2-275">Troubleshoot your implementation</span></span>

<span data-ttu-id="407d2-276">If you are experiencing issues with completing hybrid Azure AD join for domain joined Windows devices, see:</span><span class="sxs-lookup"><span data-stu-id="407d2-276">If you are experiencing issues with completing hybrid Azure AD join for domain joined Windows devices, see:</span></span>

- [<span data-ttu-id="407d2-277">Troubleshooting Hybrid Azure AD join for Windows current devices</span><span class="sxs-lookup"><span data-stu-id="407d2-277">Troubleshooting Hybrid Azure AD join for Windows current devices</span></span>](troubleshoot-hybrid-join-windows-current.md)
- [<span data-ttu-id="407d2-278">Troubleshooting Hybrid Azure AD join for Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="407d2-278">Troubleshooting Hybrid Azure AD join for Windows down-level devices</span></span>](troubleshoot-hybrid-join-windows-legacy.md)

## <a name="next-steps"></a><span data-ttu-id="407d2-279">Next steps</span><span class="sxs-lookup"><span data-stu-id="407d2-279">Next steps</span></span>

* [<span data-ttu-id="407d2-280">Introduction to device management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="407d2-280">Introduction to device management in Azure Active Directory</span></span>](overview.md)



<!--Image references-->
[1]: ./media/hybrid-azuread-join-manual-steps/12.png
