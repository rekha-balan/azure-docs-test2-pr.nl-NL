---
title: How to configure automatic registration of Windows domain-joined devices with Azure Active Directory | Microsoft Docs
description: Set up your domain-joined Windows devices to register automatically and silently with Azure Active Directory.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: markvi
ms.openlocfilehash: d27460e920dbe4482cddca6724696fee5cc897e1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662779"
---
# <a name="how-to-configure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="fde68-103">How to configure automatic registration of Windows domain-joined devices with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fde68-103">How to configure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="fde68-104">To use [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fde68-104">To use [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="fde68-105">You can get a list of registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](https://docs.microsoft.com/en-us/powershell/msonline/).</span><span class="sxs-lookup"><span data-stu-id="fde68-105">You can get a list of registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](https://docs.microsoft.com/en-us/powershell/msonline/).</span></span> 

<span data-ttu-id="fde68-106">This article provides you with the steps for configuring the automatic registration of Windows domain-joined devices with Azure AD in your organization.</span><span class="sxs-lookup"><span data-stu-id="fde68-106">This article provides you with the steps for configuring the automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="fde68-107">For more information about:</span><span class="sxs-lookup"><span data-stu-id="fde68-107">For more information about:</span></span>

- <span data-ttu-id="fde68-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fde68-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="fde68-109">Windows 10 devices in the workplace and the enhanced experiences when registered with Azure AD, see [Windows 10 for the enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fde68-109">Windows 10 devices in the workplace and the enhanced experiences when registered with Azure AD, see [Windows 10 for the enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="fde68-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="fde68-110">Before you begin</span></span>

<span data-ttu-id="fde68-111">Before you start configuring the automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span><span class="sxs-lookup"><span data-stu-id="fde68-111">Before you start configuring the automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span></span>  

<span data-ttu-id="fde68-112">To improve the readability of the descriptions, this topic uses the following term:</span><span class="sxs-lookup"><span data-stu-id="fde68-112">To improve the readability of the descriptions, this topic uses the following term:</span></span> 

- <span data-ttu-id="fde68-113">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="fde68-113">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="fde68-114">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="fde68-114">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="fde68-115">Windows current devices</span><span class="sxs-lookup"><span data-stu-id="fde68-115">Windows current devices</span></span>

- <span data-ttu-id="fde68-116">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span><span class="sxs-lookup"><span data-stu-id="fde68-116">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="fde68-117">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span><span class="sxs-lookup"><span data-stu-id="fde68-117">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="fde68-118">Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="fde68-118">Windows down-level devices</span></span>

- <span data-ttu-id="fde68-119">The following Windows down-level devices are supported:</span><span class="sxs-lookup"><span data-stu-id="fde68-119">The following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="fde68-120">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="fde68-120">Windows 8.1</span></span>
    - <span data-ttu-id="fde68-121">Windows 7</span><span class="sxs-lookup"><span data-stu-id="fde68-121">Windows 7</span></span>
    - <span data-ttu-id="fde68-122">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="fde68-122">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="fde68-123">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="fde68-123">Windows Server 2012</span></span>
    - <span data-ttu-id="fde68-124">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="fde68-124">Windows Server 2008 R2</span></span>
- <span data-ttu-id="fde68-125">The registration of Windows down-level devices **is not** supported for:</span><span class="sxs-lookup"><span data-stu-id="fde68-125">The registration of Windows down-level devices **is not** supported for:</span></span>
    - <span data-ttu-id="fde68-126">Non-federated environments (password hash sync configurations).</span><span class="sxs-lookup"><span data-stu-id="fde68-126">Non-federated environments (password hash sync configurations).</span></span>  
    - <span data-ttu-id="fde68-127">Devices using roaming profiles.</span><span class="sxs-lookup"><span data-stu-id="fde68-127">Devices using roaming profiles.</span></span> <span data-ttu-id="fde68-128">If you are relying on roaming of profiles or settings, use Windows 10.</span><span class="sxs-lookup"><span data-stu-id="fde68-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="fde68-129">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="fde68-129">Prerequisites</span></span>

<span data-ttu-id="fde68-130">Before you start enabling the auto-registration of domain-joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="fde68-130">Before you start enabling the auto-registration of domain-joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="fde68-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="fde68-131">Azure AD Connect:</span></span>

- <span data-ttu-id="fde68-132">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fde68-132">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="fde68-133">Enables other device related features like Windows Hello for Business.</span><span class="sxs-lookup"><span data-stu-id="fde68-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="fde68-134">Configuration steps</span><span class="sxs-lookup"><span data-stu-id="fde68-134">Configuration steps</span></span>

<span data-ttu-id="fde68-135">This topic includes the required steps for all typical configuration scenarios.</span><span class="sxs-lookup"><span data-stu-id="fde68-135">This topic includes the required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="fde68-136">Use the following table to get an overview of the steps that are required for your scenario:</span><span class="sxs-lookup"><span data-stu-id="fde68-136">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="fde68-137">Steps</span><span class="sxs-lookup"><span data-stu-id="fde68-137">Steps</span></span>                                      | <span data-ttu-id="fde68-138">Windows current and password hash sync</span><span class="sxs-lookup"><span data-stu-id="fde68-138">Windows current and password hash sync</span></span> | <span data-ttu-id="fde68-139">Windows current and federation</span><span class="sxs-lookup"><span data-stu-id="fde68-139">Windows current and federation</span></span> | <span data-ttu-id="fde68-140">Windows down-level</span><span class="sxs-lookup"><span data-stu-id="fde68-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="fde68-141">Step 1: Configure service connection point</span><span class="sxs-lookup"><span data-stu-id="fde68-141">Step 1: Configure service connection point</span></span> | ![Check][1]                            | ![Check][1]                    | ![Check][1]        |
| <span data-ttu-id="fde68-145">Step 2: Setup issuance of claims</span><span class="sxs-lookup"><span data-stu-id="fde68-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Check][1]                    | ![Check][1]        |
| <span data-ttu-id="fde68-148">Step 3: Enable non-Windows 10 devices</span><span class="sxs-lookup"><span data-stu-id="fde68-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Check][1]        |
| <span data-ttu-id="fde68-150">Step 4: Control deployment and rollout</span><span class="sxs-lookup"><span data-stu-id="fde68-150">Step 4: Control deployment and rollout</span></span>     | ![Check][1]                            | ![Check][1]                    | ![Check][1]        |
| <span data-ttu-id="fde68-154">Step 5: Verify registered devices</span><span class="sxs-lookup"><span data-stu-id="fde68-154">Step 5: Verify registered devices</span></span>          | ![Check][1]                            | ![Check][1]                    | ![Check][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="fde68-158">Step 1: Configure service connection point</span><span class="sxs-lookup"><span data-stu-id="fde68-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="fde68-159">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span><span class="sxs-lookup"><span data-stu-id="fde68-159">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="fde68-160">In your on-premises Active Directory (AD), the SCP object for the auto-registration of domain-joined devices must exist in the configuration naming context partition of the computer's forest.</span><span class="sxs-lookup"><span data-stu-id="fde68-160">In your on-premises Active Directory (AD), the SCP object for the auto-registration of domain-joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="fde68-161">There is only one configuration naming context per forest.</span><span class="sxs-lookup"><span data-stu-id="fde68-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="fde68-162">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span><span class="sxs-lookup"><span data-stu-id="fde68-162">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="fde68-163">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span><span class="sxs-lookup"><span data-stu-id="fde68-163">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="fde68-164">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span><span class="sxs-lookup"><span data-stu-id="fde68-164">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="fde68-165">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span><span class="sxs-lookup"><span data-stu-id="fde68-165">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="fde68-166">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span><span class="sxs-lookup"><span data-stu-id="fde68-166">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="fde68-167">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span><span class="sxs-lookup"><span data-stu-id="fde68-167">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="fde68-168">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span><span class="sxs-lookup"><span data-stu-id="fde68-168">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="fde68-169">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span><span class="sxs-lookup"><span data-stu-id="fde68-169">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span>  
<span data-ttu-id="fde68-170">The cmdlet:</span><span class="sxs-lookup"><span data-stu-id="fde68-170">The cmdlet:</span></span>

- <span data-ttu-id="fde68-171">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span><span class="sxs-lookup"><span data-stu-id="fde68-171">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="fde68-172">Requires you to specify the `AdConnectorAccount` parameter.</span><span class="sxs-lookup"><span data-stu-id="fde68-172">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="fde68-173">This is the account that is configured as Active Directory connector account in Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="fde68-173">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="fde68-174">The following script shows an example for using the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fde68-174">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="fde68-175">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span><span class="sxs-lookup"><span data-stu-id="fde68-175">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="fde68-176">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="fde68-176">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="fde68-177">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span><span class="sxs-lookup"><span data-stu-id="fde68-177">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="fde68-178">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span><span class="sxs-lookup"><span data-stu-id="fde68-178">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span> 

<span data-ttu-id="fde68-179">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span><span class="sxs-lookup"><span data-stu-id="fde68-179">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="fde68-180">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span><span class="sxs-lookup"><span data-stu-id="fde68-180">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="fde68-181">Step 2: Setup issuance of claims</span><span class="sxs-lookup"><span data-stu-id="fde68-181">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="fde68-182">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fde68-182">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="fde68-183">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="fde68-183">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="fde68-184">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span><span class="sxs-lookup"><span data-stu-id="fde68-184">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="fde68-185">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span><span class="sxs-lookup"><span data-stu-id="fde68-185">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="fde68-186">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span><span class="sxs-lookup"><span data-stu-id="fde68-186">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="fde68-187">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="fde68-187">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="fde68-188">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span><span class="sxs-lookup"><span data-stu-id="fde68-188">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="fde68-189">The following claims must exist in the token received by Azure DRS for device registration to complete.</span><span class="sxs-lookup"><span data-stu-id="fde68-189">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="fde68-190">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span><span class="sxs-lookup"><span data-stu-id="fde68-190">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="fde68-191">If you have more than one verified domain name, you need to provide the following claim for computers:</span><span class="sxs-lookup"><span data-stu-id="fde68-191">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="fde68-192">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span><span class="sxs-lookup"><span data-stu-id="fde68-192">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="fde68-193">In the following sections, you find information about:</span><span class="sxs-lookup"><span data-stu-id="fde68-193">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="fde68-194">The values each claim should have</span><span class="sxs-lookup"><span data-stu-id="fde68-194">The values each claim should have</span></span>
- <span data-ttu-id="fde68-195">How a definition would look like in AD FS</span><span class="sxs-lookup"><span data-stu-id="fde68-195">How a definition would look like in AD FS</span></span>

<span data-ttu-id="fde68-196">The definition helps you to verify whether the values are present or if you need to create them.</span><span class="sxs-lookup"><span data-stu-id="fde68-196">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="fde68-197">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span><span class="sxs-lookup"><span data-stu-id="fde68-197">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="fde68-198">Issue account type claim</span><span class="sxs-lookup"><span data-stu-id="fde68-198">Issue account type claim</span></span>

<span data-ttu-id="fde68-199">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span><span class="sxs-lookup"><span data-stu-id="fde68-199">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="fde68-200">In AD FS, you can add an issuance transform rule that looks like this:</span><span class="sxs-lookup"><span data-stu-id="fde68-200">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="fde68-201">Issue objectGUID of the computer account on-premises</span><span class="sxs-lookup"><span data-stu-id="fde68-201">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="fde68-202">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span><span class="sxs-lookup"><span data-stu-id="fde68-202">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="fde68-203">In AD FS, you can add an issuance transform rule that looks like this:</span><span class="sxs-lookup"><span data-stu-id="fde68-203">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="fde68-204">Issue objectSID of the computer account on-premises</span><span class="sxs-lookup"><span data-stu-id="fde68-204">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="fde68-205">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span><span class="sxs-lookup"><span data-stu-id="fde68-205">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="fde68-206">In AD FS, you can add an issuance transform rule that looks like this:</span><span class="sxs-lookup"><span data-stu-id="fde68-206">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="fde68-207">Issue issuerID for computer when multiple verified domain names in Azure AD</span><span class="sxs-lookup"><span data-stu-id="fde68-207">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="fde68-208">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span><span class="sxs-lookup"><span data-stu-id="fde68-208">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="fde68-209">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span><span class="sxs-lookup"><span data-stu-id="fde68-209">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="fde68-210">Please note that one rule to explicitly issue the rule for users is necessary.</span><span class="sxs-lookup"><span data-stu-id="fde68-210">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="fde68-211">In the rules below, a first rule identifying user vs. computer authentication is added.</span><span class="sxs-lookup"><span data-stu-id="fde68-211">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

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


<span data-ttu-id="fde68-212">In the claim above,</span><span class="sxs-lookup"><span data-stu-id="fde68-212">In the claim above,</span></span>

- <span data-ttu-id="fde68-213">`$<domain>` is the AD FS service URL</span><span class="sxs-lookup"><span data-stu-id="fde68-213">`$<domain>` is the AD FS service URL</span></span>
- <span data-ttu-id="fde68-214">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span><span class="sxs-lookup"><span data-stu-id="fde68-214">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="fde68-215">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="fde68-215">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="fde68-216">To get a list of your verified company domains, you can use the [Get-MsolDomain](https://docs.microsoft.com/powershell/msonline/v1/get-msoldomain) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fde68-216">To get a list of your verified company domains, you can use the [Get-MsolDomain](https://docs.microsoft.com/powershell/msonline/v1/get-msoldomain) cmdlet.</span></span> 

![Get-MsolDomain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="fde68-218">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span><span class="sxs-lookup"><span data-stu-id="fde68-218">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="fde68-219">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span><span class="sxs-lookup"><span data-stu-id="fde68-219">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="fde68-220">In AD FS, you can create an issuance transform rule as follows:</span><span class="sxs-lookup"><span data-stu-id="fde68-220">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="fde68-221">Helper script to create the AD FS issuance transform rules</span><span class="sxs-lookup"><span data-stu-id="fde68-221">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="fde68-222">The following script helps you with the creation of the issuance transform rules described above.</span><span class="sxs-lookup"><span data-stu-id="fde68-222">The following script helps you with the creation of the issuance transform rules described above.</span></span>

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
        Value = "http://<verified-domain-name>/adfs/services/trust/"
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

### <a name="remarks"></a><span data-ttu-id="fde68-223">Remarks</span><span class="sxs-lookup"><span data-stu-id="fde68-223">Remarks</span></span> 

- <span data-ttu-id="fde68-224">This script appends the rules to the existing rules.</span><span class="sxs-lookup"><span data-stu-id="fde68-224">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="fde68-225">Do not run the script twice because the set of rules would be added twice.</span><span class="sxs-lookup"><span data-stu-id="fde68-225">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="fde68-226">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span><span class="sxs-lookup"><span data-stu-id="fde68-226">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="fde68-227">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span><span class="sxs-lookup"><span data-stu-id="fde68-227">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="fde68-228">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span><span class="sxs-lookup"><span data-stu-id="fde68-228">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="fde68-229">Here is an example for this rule:</span><span class="sxs-lookup"><span data-stu-id="fde68-229">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="fde68-230">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$oneOfVerifiedDomainNames** in the script to **$true**.</span><span class="sxs-lookup"><span data-stu-id="fde68-230">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$oneOfVerifiedDomainNames** in the script to **$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="fde68-231">Step 3: Enable Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="fde68-231">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="fde68-232">If some of your domain-joined devices Windows down-level devices, you need to:</span><span class="sxs-lookup"><span data-stu-id="fde68-232">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="fde68-233">Set a policy in Azure AD to enable users to register devices.</span><span class="sxs-lookup"><span data-stu-id="fde68-233">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="fde68-234">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span><span class="sxs-lookup"><span data-stu-id="fde68-234">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="fde68-235">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span><span class="sxs-lookup"><span data-stu-id="fde68-235">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="fde68-236">Set policy in Azure AD to enable users to register devices</span><span class="sxs-lookup"><span data-stu-id="fde68-236">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="fde68-237">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span><span class="sxs-lookup"><span data-stu-id="fde68-237">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="fde68-238">In the Azure portal, you can find this setting under:</span><span class="sxs-lookup"><span data-stu-id="fde68-238">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="fde68-239">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span><span class="sxs-lookup"><span data-stu-id="fde68-239">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Register devices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="fde68-241">Configure on-premises federation service</span><span class="sxs-lookup"><span data-stu-id="fde68-241">Configure on-premises federation service</span></span> 

<span data-ttu-id="fde68-242">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span><span class="sxs-lookup"><span data-stu-id="fde68-242">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="fde68-243">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span><span class="sxs-lookup"><span data-stu-id="fde68-243">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="fde68-244">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span><span class="sxs-lookup"><span data-stu-id="fde68-244">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="fde68-245">**To add this rule:**</span><span class="sxs-lookup"><span data-stu-id="fde68-245">**To add this rule:**</span></span>

1. <span data-ttu-id="fde68-246">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="fde68-246">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="fde68-247">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span><span class="sxs-lookup"><span data-stu-id="fde68-247">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="fde68-248">On the **Issuance Transform Rules** tab, select **Add Rule**.</span><span class="sxs-lookup"><span data-stu-id="fde68-248">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="fde68-249">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span><span class="sxs-lookup"><span data-stu-id="fde68-249">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="fde68-250">Select **Next**.</span><span class="sxs-lookup"><span data-stu-id="fde68-250">Select **Next**.</span></span>
6. <span data-ttu-id="fde68-251">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span><span class="sxs-lookup"><span data-stu-id="fde68-251">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="fde68-252">In the **Claim rule** box, type the following rule:</span><span class="sxs-lookup"><span data-stu-id="fde68-252">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="fde68-253">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span><span class="sxs-lookup"><span data-stu-id="fde68-253">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="fde68-254">This object usually is named **Microsoft Office 365 Identity Platform**.</span><span class="sxs-lookup"><span data-stu-id="fde68-254">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="fde68-255">Add the Azure AD device authentication end-point to the Local Intranet zones</span><span class="sxs-lookup"><span data-stu-id="fde68-255">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="fde68-256">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="fde68-256">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="fde68-257">Step 4: Control deployment and rollout</span><span class="sxs-lookup"><span data-stu-id="fde68-257">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="fde68-258">When you have completed the required steps, domain-joined devices are ready to automatically register with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fde68-258">When you have completed the required steps, domain-joined devices are ready to automatically register with Azure AD.</span></span> <span data-ttu-id="fde68-259">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span><span class="sxs-lookup"><span data-stu-id="fde68-259">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="fde68-260">New devices register with Azure AD when the device restarts after the domain join operation completes.</span><span class="sxs-lookup"><span data-stu-id="fde68-260">New devices register with Azure AD when the device restarts after the domain join operation completes.</span></span>

### <a name="remarks"></a><span data-ttu-id="fde68-261">Remarks</span><span class="sxs-lookup"><span data-stu-id="fde68-261">Remarks</span></span>

- <span data-ttu-id="fde68-262">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span><span class="sxs-lookup"><span data-stu-id="fde68-262">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="fde68-263">Windows 10 November 2015 Update automatically registers with Azure AD **only** if the rollout Group Policy object is set.</span><span class="sxs-lookup"><span data-stu-id="fde68-263">Windows 10 November 2015 Update automatically registers with Azure AD **only** if the rollout Group Policy object is set.</span></span>

- <span data-ttu-id="fde68-264">To rollout the automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span><span class="sxs-lookup"><span data-stu-id="fde68-264">To rollout the automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span></span>

- <span data-ttu-id="fde68-265">If you push the Group Policy object to Windows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to register all your Windows down-level devices.</span><span class="sxs-lookup"><span data-stu-id="fde68-265">If you push the Group Policy object to Windows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to register all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="fde68-266">Create a Group Policy object</span><span class="sxs-lookup"><span data-stu-id="fde68-266">Create a Group Policy object</span></span> 

<span data-ttu-id="fde68-267">To control the rollout of automatic registration of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span><span class="sxs-lookup"><span data-stu-id="fde68-267">To control the rollout of automatic registration of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span></span> <span data-ttu-id="fde68-268">For example, you can deploy the policy to an organizational unit or to a security group.</span><span class="sxs-lookup"><span data-stu-id="fde68-268">For example, you can deploy the policy to an organizational unit or to a security group.</span></span>

<span data-ttu-id="fde68-269">**To set the policy:**</span><span class="sxs-lookup"><span data-stu-id="fde68-269">**To set the policy:**</span></span>

1. <span data-ttu-id="fde68-270">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="fde68-270">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="fde68-271">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span><span class="sxs-lookup"><span data-stu-id="fde68-271">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="fde68-272">Right-click **Group Policy Objects**, and then select **New**.</span><span class="sxs-lookup"><span data-stu-id="fde68-272">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="fde68-273">Type a name for your Group Policy object.</span><span class="sxs-lookup"><span data-stu-id="fde68-273">Type a name for your Group Policy object.</span></span> <span data-ttu-id="fde68-274">For example, *Automatic Registration to Azure AD*.</span><span class="sxs-lookup"><span data-stu-id="fde68-274">For example, *Automatic Registration to Azure AD*.</span></span> <span data-ttu-id="fde68-275">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="fde68-275">Select **OK**.</span></span>
5. <span data-ttu-id="fde68-276">Right-click your new Group Policy object, and then select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="fde68-276">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="fde68-277">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span><span class="sxs-lookup"><span data-stu-id="fde68-277">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="fde68-278">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="fde68-278">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fde68-279">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span><span class="sxs-lookup"><span data-stu-id="fde68-279">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="fde68-280">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="fde68-280">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="fde68-281">Select **Enabled**, and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="fde68-281">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="fde68-282">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="fde68-282">Select **OK**.</span></span>
9. <span data-ttu-id="fde68-283">Link the Group Policy object to a location of your choice.</span><span class="sxs-lookup"><span data-stu-id="fde68-283">Link the Group Policy object to a location of your choice.</span></span> <span data-ttu-id="fde68-284">For example, you can link it to a specific organizational unit.</span><span class="sxs-lookup"><span data-stu-id="fde68-284">For example, you can link it to a specific organizational unit.</span></span> <span data-ttu-id="fde68-285">You also could link it to a specific security group of computers that automatically register with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fde68-285">You also could link it to a specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="fde68-286">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span><span class="sxs-lookup"><span data-stu-id="fde68-286">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="fde68-287">Windows Installer packages for non-Windows 10 computers</span><span class="sxs-lookup"><span data-stu-id="fde68-287">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="fde68-288">To register domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span><span class="sxs-lookup"><span data-stu-id="fde68-288">To register domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="fde68-289">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="fde68-289">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="fde68-290">The package supports the standard silent install options with the *quiet* parameter.</span><span class="sxs-lookup"><span data-stu-id="fde68-290">The package supports the standard silent install options with the *quiet* parameter.</span></span> <span data-ttu-id="fde68-291">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span><span class="sxs-lookup"><span data-stu-id="fde68-291">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span> <span data-ttu-id="fde68-292">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="fde68-292">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="fde68-293">The installer creates a scheduled task on the system that runs in the user’s context.</span><span class="sxs-lookup"><span data-stu-id="fde68-293">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="fde68-294">The task is triggered when the user signs in to Windows.</span><span class="sxs-lookup"><span data-stu-id="fde68-294">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="fde68-295">The task silently registers the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="fde68-295">The task silently registers the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="fde68-296">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span><span class="sxs-lookup"><span data-stu-id="fde68-296">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="fde68-297">Step 5: Verify registered devices</span><span class="sxs-lookup"><span data-stu-id="fde68-297">Step 5: Verify registered devices</span></span>

<span data-ttu-id="fde68-298">You can check successful registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](https://docs.microsoft.com/en-us/powershell/msonline/).</span><span class="sxs-lookup"><span data-stu-id="fde68-298">You can check successful registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](https://docs.microsoft.com/en-us/powershell/msonline/).</span></span>

<span data-ttu-id="fde68-299">The output of this cmdlet shows devices registered in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fde68-299">The output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="fde68-300">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span><span class="sxs-lookup"><span data-stu-id="fde68-300">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="fde68-301">Domain joined devices have a value of **Domain Joined**.</span><span class="sxs-lookup"><span data-stu-id="fde68-301">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fde68-302">Next steps</span><span class="sxs-lookup"><span data-stu-id="fde68-302">Next steps</span></span>

* [<span data-ttu-id="fde68-303">Automatic device registration FAQ</span><span class="sxs-lookup"><span data-stu-id="fde68-303">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="fde68-304">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="fde68-304">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="fde68-305">Troubleshooting auto-registration of domain joined computers to Azure AD – non-Windows 10</span><span class="sxs-lookup"><span data-stu-id="fde68-305">Troubleshooting auto-registration of domain joined computers to Azure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="fde68-306">Azure Active Directory conditional access</span><span class="sxs-lookup"><span data-stu-id="fde68-306">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-automatic-device-registration-setup/12.png



