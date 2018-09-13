---
title: Troubleshooting the auto-registration of Azure AD domain joined computers for Windows 10 and Windows Server 2016| Microsoft Docs
description: Troubleshooting the auto-registration of Azure AD domain joined computers for Windows 10 and Windows Server 2016.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: markvi
ms.openlocfilehash: 2faf328e6622b9a1e3b529d62b61061659041fbd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540945"
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="2f580-103">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2f580-103">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="2f580-104">This topic is applicable to the following clients:</span><span class="sxs-lookup"><span data-stu-id="2f580-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="2f580-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="2f580-105">Windows 10</span></span>
-   <span data-ttu-id="2f580-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2f580-106">Windows Server 2016</span></span>

<span data-ttu-id="2f580-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="2f580-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="2f580-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) to support the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="2f580-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) to support the following scenarios:</span></span>

- [<span data-ttu-id="2f580-109">Device-based conditional access</span><span class="sxs-lookup"><span data-stu-id="2f580-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="2f580-110">Enterprise roaming of settings</span><span class="sxs-lookup"><span data-stu-id="2f580-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="2f580-111">Windows Hello for Business</span><span class="sxs-lookup"><span data-stu-id="2f580-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="2f580-112">This document provides troubleshooting guidance on how to resolve potential issues.</span><span class="sxs-lookup"><span data-stu-id="2f580-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 

<span data-ttu-id="2f580-113">The registration is supported in the Windows 10 November 2015 Update and above.</span><span class="sxs-lookup"><span data-stu-id="2f580-113">The registration is supported in the Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="2f580-114">We recommend using the Anniversary Update for enabling the scenarios above.</span><span class="sxs-lookup"><span data-stu-id="2f580-114">We recommend using the Anniversary Update for enabling the scenarios above.</span></span>

## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="2f580-115">Step 1: Retrieve the registration status</span><span class="sxs-lookup"><span data-stu-id="2f580-115">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="2f580-116">**To retrieve the registration status:**</span><span class="sxs-lookup"><span data-stu-id="2f580-116">**To retrieve the registration status:**</span></span>

1. <span data-ttu-id="2f580-117">Open the command prompt as an administrator.</span><span class="sxs-lookup"><span data-stu-id="2f580-117">Open the command prompt as an administrator.</span></span>

2. <span data-ttu-id="2f580-118">Type **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="2f580-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="2f580-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="2f580-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="2f580-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="2f580-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="2f580-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="2f580-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="2f580-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="2f580-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="2f580-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="2f580-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="2f580-124">Step 2: Evaluate the registration status</span><span class="sxs-lookup"><span data-stu-id="2f580-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="2f580-125">Review the following fields and make sure that they have the expected values:</span><span class="sxs-lookup"><span data-stu-id="2f580-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="2f580-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="2f580-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="2f580-127">This field shows whether the device is registered with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f580-127">This field shows whether the device is registered with Azure AD.</span></span> <span data-ttu-id="2f580-128">If the value shows as ‘NO’, registration has not completed.</span><span class="sxs-lookup"><span data-stu-id="2f580-128">If the value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="2f580-129">**Possible causes:**</span><span class="sxs-lookup"><span data-stu-id="2f580-129">**Possible causes:**</span></span>

- <span data-ttu-id="2f580-130">Authentication of the computer for registration failed.</span><span class="sxs-lookup"><span data-stu-id="2f580-130">Authentication of the computer for registration failed.</span></span>

- <span data-ttu-id="2f580-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span><span class="sxs-lookup"><span data-stu-id="2f580-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="2f580-132">The computer cannot reach Azure AD for authentication or Azure DRS for registration</span><span class="sxs-lookup"><span data-stu-id="2f580-132">The computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="2f580-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span><span class="sxs-lookup"><span data-stu-id="2f580-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="2f580-134">If the computer has a TPM, it may be in a bad state.</span><span class="sxs-lookup"><span data-stu-id="2f580-134">If the computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="2f580-135">There may be a misconfiguration in services noted in the document earlier that you will need to verify again.</span><span class="sxs-lookup"><span data-stu-id="2f580-135">There may be a misconfiguration in services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="2f580-136">Common examples are:</span><span class="sxs-lookup"><span data-stu-id="2f580-136">Common examples are:</span></span>

    - <span data-ttu-id="2f580-137">Your federation server does not have WS-Trust endpoints enabled</span><span class="sxs-lookup"><span data-stu-id="2f580-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="2f580-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="2f580-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="2f580-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span><span class="sxs-lookup"><span data-stu-id="2f580-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="2f580-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="2f580-140">DomainJoined : YES</span></span>  

<span data-ttu-id="2f580-141">This field shows whether the device is joined to an on-premises Active Directory or not.</span><span class="sxs-lookup"><span data-stu-id="2f580-141">This field shows whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="2f580-142">If the value shows as **NO**, the device cannot auto-register with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f580-142">If the value shows as **NO**, the device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="2f580-143">Check first that the device joins to the on-premises Active Directory before it can register with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f580-143">Check first that the device joins to the on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="2f580-144">If you are looking for joining the computer to Azure AD directly, please go to Learn about capabilities of Azure Active Directory Join.</span><span class="sxs-lookup"><span data-stu-id="2f580-144">If you are looking for joining the computer to Azure AD directly, please go to Learn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="2f580-145">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="2f580-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="2f580-146">This field shows whether the device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span><span class="sxs-lookup"><span data-stu-id="2f580-146">This field shows whether the device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="2f580-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior to the computer completing registration.</span><span class="sxs-lookup"><span data-stu-id="2f580-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior to the computer completing registration.</span></span> <span data-ttu-id="2f580-148">In this case the account will be ignored if using the Anniversary Update version of Windows 10 (1607 when running the WinVer command in the ‘Run’ window or a command prompt window).</span><span class="sxs-lookup"><span data-stu-id="2f580-148">In this case the account will be ignored if using the Anniversary Update version of Windows 10 (1607 when running the WinVer command in the ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="2f580-149">WamDefaultSet : YES and AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="2f580-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="2f580-150">These fields show that the user has successfully authenticated to Azure AD upon signing in to the device.</span><span class="sxs-lookup"><span data-stu-id="2f580-150">These fields show that the user has successfully authenticated to Azure AD upon signing in to the device.</span></span> <span data-ttu-id="2f580-151">If they show ‘NO’ the following are possible causes:</span><span class="sxs-lookup"><span data-stu-id="2f580-151">If they show ‘NO’ the following are possible causes:</span></span>

- <span data-ttu-id="2f580-152">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span><span class="sxs-lookup"><span data-stu-id="2f580-152">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="2f580-153">Alternate Login ID</span><span class="sxs-lookup"><span data-stu-id="2f580-153">Alternate Login ID</span></span>

- <span data-ttu-id="2f580-154">HTTP Proxy not found</span><span class="sxs-lookup"><span data-stu-id="2f580-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f580-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f580-155">Next steps</span></span>

<span data-ttu-id="2f580-156">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="2f580-156">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 