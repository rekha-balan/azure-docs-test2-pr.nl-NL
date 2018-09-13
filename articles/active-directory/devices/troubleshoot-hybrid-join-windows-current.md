---
title: Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices| Microsoft Docs
description: Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.component: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d96c1e8adee55127a50b2d7c374418c22bfec4c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967828"
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="dd187-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span><span class="sxs-lookup"><span data-stu-id="dd187-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="dd187-104">This article is applicable to the following clients:</span><span class="sxs-lookup"><span data-stu-id="dd187-104">This article is applicable to the following clients:</span></span>

-   <span data-ttu-id="dd187-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="dd187-105">Windows 10</span></span>
-   <span data-ttu-id="dd187-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="dd187-106">Windows Server 2016</span></span>

<span data-ttu-id="dd187-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](troubleshoot-hybrid-join-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="dd187-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="dd187-108">This article assumes that you have [configured hybrid Azure Active Directory joined devices](hybrid-azuread-join-plan.md) to support the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="dd187-108">This article assumes that you have [configured hybrid Azure Active Directory joined devices](hybrid-azuread-join-plan.md) to support the following scenarios:</span></span>

- <span data-ttu-id="dd187-109">Device-based conditional access</span><span class="sxs-lookup"><span data-stu-id="dd187-109">Device-based conditional access</span></span>

- [<span data-ttu-id="dd187-110">Enterprise roaming of settings</span><span class="sxs-lookup"><span data-stu-id="dd187-110">Enterprise roaming of settings</span></span>](../active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="dd187-111">Windows Hello for Business</span><span class="sxs-lookup"><span data-stu-id="dd187-111">Windows Hello for Business</span></span>](../active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="dd187-112">This document provides troubleshooting guidance on how to resolve potential issues.</span><span class="sxs-lookup"><span data-stu-id="dd187-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 


<span data-ttu-id="dd187-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports the Windows 10 November 2015 Update and above.</span><span class="sxs-lookup"><span data-stu-id="dd187-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports the Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="dd187-114">We recommend using the Anniversary update.</span><span class="sxs-lookup"><span data-stu-id="dd187-114">We recommend using the Anniversary update.</span></span>

## <a name="step-1-retrieve-the-join-status"></a><span data-ttu-id="dd187-115">Step 1: Retrieve the join status</span><span class="sxs-lookup"><span data-stu-id="dd187-115">Step 1: Retrieve the join status</span></span> 

<span data-ttu-id="dd187-116">**To retrieve the join status:**</span><span class="sxs-lookup"><span data-stu-id="dd187-116">**To retrieve the join status:**</span></span>

1. <span data-ttu-id="dd187-117">Open the command prompt as an administrator</span><span class="sxs-lookup"><span data-stu-id="dd187-117">Open the command prompt as an administrator</span></span>

2. <span data-ttu-id="dd187-118">Type **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="dd187-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="dd187-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="dd187-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="dd187-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="dd187-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="dd187-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="dd187-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="dd187-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="dd187-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="dd187-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span><span class="sxs-lookup"><span data-stu-id="dd187-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-the-join-status"></a><span data-ttu-id="dd187-124">Step 2: Evaluate the join status</span><span class="sxs-lookup"><span data-stu-id="dd187-124">Step 2: Evaluate the join status</span></span> 

<span data-ttu-id="dd187-125">Review the following fields and make sure that they have the expected values:</span><span class="sxs-lookup"><span data-stu-id="dd187-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="dd187-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="dd187-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="dd187-127">This field indicates whether the device is joined with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd187-127">This field indicates whether the device is joined with Azure AD.</span></span> <span data-ttu-id="dd187-128">If the value is **NO**, the join to Azure AD has not completed yet.</span><span class="sxs-lookup"><span data-stu-id="dd187-128">If the value is **NO**, the join to Azure AD has not completed yet.</span></span> 

<span data-ttu-id="dd187-129">**Possible causes:**</span><span class="sxs-lookup"><span data-stu-id="dd187-129">**Possible causes:**</span></span>

- <span data-ttu-id="dd187-130">Authentication of the computer for a join failed.</span><span class="sxs-lookup"><span data-stu-id="dd187-130">Authentication of the computer for a join failed.</span></span>

- <span data-ttu-id="dd187-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span><span class="sxs-lookup"><span data-stu-id="dd187-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="dd187-132">The computer cannot reach Azure AD to authenticate or Azure DRS for registration</span><span class="sxs-lookup"><span data-stu-id="dd187-132">The computer cannot reach Azure AD to authenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="dd187-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span><span class="sxs-lookup"><span data-stu-id="dd187-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="dd187-134">If the computer has a TPM, it can be in a bad state.</span><span class="sxs-lookup"><span data-stu-id="dd187-134">If the computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="dd187-135">There might be a misconfiguration in the services noted in the document earlier that you will need to verify again.</span><span class="sxs-lookup"><span data-stu-id="dd187-135">There might be a misconfiguration in the services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="dd187-136">Common examples are:</span><span class="sxs-lookup"><span data-stu-id="dd187-136">Common examples are:</span></span>

    - <span data-ttu-id="dd187-137">Your federation server does not have WS-Trust endpoints enabled</span><span class="sxs-lookup"><span data-stu-id="dd187-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="dd187-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="dd187-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="dd187-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span><span class="sxs-lookup"><span data-stu-id="dd187-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="dd187-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="dd187-140">DomainJoined : YES</span></span>  

<span data-ttu-id="dd187-141">This field indicates whether the device is joined to an on-premises Active Directory or not.</span><span class="sxs-lookup"><span data-stu-id="dd187-141">This field indicates whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="dd187-142">If the value is **NO**, the device cannot perform a hybrid Azure AD join.</span><span class="sxs-lookup"><span data-stu-id="dd187-142">If the value is **NO**, the device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="dd187-143">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="dd187-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="dd187-144">This field indicates whether the device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span><span class="sxs-lookup"><span data-stu-id="dd187-144">This field indicates whether the device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="dd187-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span><span class="sxs-lookup"><span data-stu-id="dd187-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="dd187-146">If the value is **YES**, a work or school account was added prior to the completion of the hybrid Azure AD join.</span><span class="sxs-lookup"><span data-stu-id="dd187-146">If the value is **YES**, a work or school account was added prior to the completion of the hybrid Azure AD join.</span></span> <span data-ttu-id="dd187-147">In this case, the account is ignored when using the Anniversary Update version of Windows 10 (1607).</span><span class="sxs-lookup"><span data-stu-id="dd187-147">In this case, the account is ignored when using the Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="dd187-148">WamDefaultSet : YES and AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="dd187-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="dd187-149">These fields indicate whether the user has successfully authenticated to Azure AD when signing in to the device.</span><span class="sxs-lookup"><span data-stu-id="dd187-149">These fields indicate whether the user has successfully authenticated to Azure AD when signing in to the device.</span></span> <span data-ttu-id="dd187-150">If the values are **NO**, it could be due:</span><span class="sxs-lookup"><span data-stu-id="dd187-150">If the values are **NO**, it could be due:</span></span>

- <span data-ttu-id="dd187-151">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span><span class="sxs-lookup"><span data-stu-id="dd187-151">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="dd187-152">Alternate Login ID</span><span class="sxs-lookup"><span data-stu-id="dd187-152">Alternate Login ID</span></span>

- <span data-ttu-id="dd187-153">HTTP Proxy not found</span><span class="sxs-lookup"><span data-stu-id="dd187-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd187-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="dd187-154">Next steps</span></span>

<span data-ttu-id="dd187-155">For questions, see the [device management FAQ](faq.md)</span><span class="sxs-lookup"><span data-stu-id="dd187-155">For questions, see the [device management FAQ](faq.md)</span></span> 